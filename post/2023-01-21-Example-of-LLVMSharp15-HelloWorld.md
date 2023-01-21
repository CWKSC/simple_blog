# Example of LLVMSharp15 - HelloWorld

Create a new C# console project, and install libLLVM and LLVMSharp by NuGet (remember to check the pre-release checkbox)

Add `<AllowUnsafeBlocks>true</AllowUnsafeBlocks>` and `<RuntimeIdentifier Condition="'$(RuntimeIdentifier)' == ''">$(NETCoreSdkRuntimeIdentifier)</RuntimeIdentifier>` in to `.csproj` under `<PropertyGroup>`

The `.csproj` should like:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net7.0</TargetFramework>
    <ImplicitUsings>enable</ImplicitUsings>
    <Nullable>enable</Nullable>
	<AllowUnsafeBlocks>true</AllowUnsafeBlocks>
	<RuntimeIdentifier Condition="'$(RuntimeIdentifier)' == ''">$(NETCoreSdkRuntimeIdentifier)</RuntimeIdentifier>
  </PropertyGroup>

  <ItemGroup>
	<PackageReference Include="libLLVM" Version="15.0.0" />
	<PackageReference Include="LLVMSharp" Version="15.0.0-beta1" />
  </ItemGroup>

</Project>
```

Since the API needs to use `sbyte*`, `LLVMOpaqueType**`, and `LLVMOpaqueValue**`, we create some utility functions:

```cs
// string to sbyte* //
public static unsafe sbyte* ToSbytePointer(this string value)
{
    byte[] bytes = new byte[Encoding.Default.GetByteCount(value) + 1];
    Encoding.Default.GetBytes(value, 0, value.Length, bytes, 0);
    fixed (byte* b = bytes) { return (sbyte*)b; }
}

// LLVMOpaqueType*[] to LLVMOpaqueType** //
public static unsafe LLVMOpaqueType** ToLLVMOpaqueTypePtrPtr(this LLVMOpaqueType*[] values)
{
    fixed (LLVMOpaqueType** temp = values) { return temp; }
}

// LLVMOpaqueValue*[] to LLVMOpaqueValue** //
public static unsafe LLVMOpaqueValue** ToLLVMOpaqueValuePtrPtr(this LLVMOpaqueValue*[] values)
{
    fixed (LLVMOpaqueValue** temp = values) { return temp; }
}
```

Create context and module

```cs
// Context and Module //
var context = LLVM.ContextCreate();
var module  = LLVM.ModuleCreateWithNameInContext("Hello World".ToSbytePointer(), context);
```

Declare puts function

```cs
// Declare i32 @puts(ptr %0) //
var putsReturnTy    = LLVM.Int32Type();
var putsName        = "puts".ToSbytePointer();
var putsArgTys      = new[] { LLVM.PointerType(LLVM.Int8Type(), 0) };
var putsArgTyPtrPtr = putsArgTys.ToLLVMOpaqueTypePtrPtr();
var putsFuncTy      = LLVM.FunctionType(putsReturnTy, putsArgTyPtrPtr, (uint)putsArgTys.Length, 0);
var putsFunc        = LLVM.AddFunction(module, putsName, putsFuncTy);
LLVM.SetLinkage(putsFunc, LLVMLinkage.LLVMExternalLinkage);
```

Declare main function

```cs
// Declare i32 @main() //
var mainName         = "main".ToSbytePointer();
var mainReturnTy     = LLVM.Int32Type();
var mainArgTys       = new LLVMOpaqueType*[] { };
var mainArgTysPtrPtr = mainArgTys.ToLLVMOpaqueTypePtrPtr();
var mainFuncTy       = LLVM.FunctionType(mainReturnTy, mainArgTysPtrPtr, (uint)mainArgTys.Length, 0);
var mainFunc         = LLVM.AddFunction(module, mainName, mainFuncTy);
```

Create basic block under main function

```cs
// Create entry basic block in main //
var entry   = LLVM.AppendBasicBlock(mainFunc, "entry".ToSbytePointer());
var builder = LLVM.CreateBuilder();
LLVM.PositionBuilderAtEnd(builder, entry);
```

Create global string - `"Hello World!"`

```cs
// Create global string //
var helloWorldString       = "Hello World!".ToSbytePointer();
var helloWorldGlobalString = LLVM.BuildGlobalStringPtr(builder, helloWorldString, "".ToSbytePointer());
```

Create call inst

```cs
// Create function call inst //
var callArgs = new[] { helloWorldGlobalString };
var callArgsPtrPtr = callArgs.ToLLVMOpaqueValuePtrPtr();
_ = LLVM.BuildCall2(builder, putsFuncTy, putsFunc, callArgsPtrPtr, (uint)callArgs.Length, "".ToSbytePointer());
```

Create ret inst 

```cs
// Create return inst //
var constInt0 = LLVM.ConstInt(LLVM.Int32Type(), 0, 1);
_ = LLVM.BuildRet(builder, constInt0);
```

Output the LLVM IR

```cs
// Output LLVM IR //
Console.WriteLine("[Output of LLVM IR]:\n");
Console.WriteLine(new string(LLVM.PrintModuleToString(module)));
// Or LLVM.DumpModule(module);
```

```llvm
[Output of LLVM IR]:

; ModuleID = 'Hello World'
source_filename = "Hello World"

@0 = private unnamed_addr constant [13 x i8] c"Hello World!\00", align 1

declare i32 @puts(ptr %0)

define i32 @main() {
entry:
  %0 = call i32 @puts(ptr @0)
  ret i32 0
}
```

Run LLVM IR by Execution Engine 

```cs
LLVM.LinkInMCJIT();
LLVM.InitializeX86TargetMC();

LLVM.InitializeX86Target();
LLVM.InitializeX86TargetInfo();
LLVM.InitializeX86AsmParser();
LLVM.InitializeX86AsmPrinter();

LLVMOpaqueExecutionEngine* outEE = null;
sbyte* outError = null;
_ = LLVM.CreateExecutionEngineForModule(&outEE, module, &outError);
var main = LLVM.GetNamedFunction(module, "main".ToSbytePointer());
LLVM.RunFunction(outEE, main, 0, null);
```

```
[Output of JIT Compiler]:

Hello World!
```