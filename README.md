# OpenAssetImporter Library Binding for Zig

This repo packages [Assimp](https://github.com/assimp/assimp) 5.4.0 for the Zig build system (requires Zig 0.17.0).

## Add the dependency

```sh
zig fetch --save git+https://github.com/allyourcodebase/assimp.git
```

Or add it manually to `build.zig.zon`:

```zig
.dependencies = .{
    .zig_assimp = .{
        .url = "https://github.com/allyourcodebase/assimp/archive/<commit>.tar.gz",
        .hash = "...",
    },
},
```

## Use it in `build.zig`

```zig
const assimp_dep = b.dependency("zig_assimp", .{
    .target = target,
    .optimize = optimize,
    .formats = @as([]const u8, "STL,Obj,FBX"), // or "all"
    .double = false,
});

exe.addImport("assimp" assimp_dep.module("assimp"));
```

## Options

- `formats` — comma-separated list of importers/exporters to compile, or `all`. Empty (default) builds none. See `build.zig` for the full list.
- `double` — store data as `double` instead of `float`.
