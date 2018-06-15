---
Description: Describes a volume.
ms.assetid: c0224f4e-3d32-4bdd-b56c-4e8aa291bb27
title: D3DVOLUME\_DESC structure
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: structure
ms.date: 05/31/2018
---

# D3DVOLUME\_DESC structure

Describes a volume.

## Syntax


```C++
typedef struct D3DVOLUME_DESC {
  D3DFORMAT       Format;
  D3DRESOURCETYPE Type;
  DWORD           Usage;
  D3DPOOL         Pool;
  UINT            Width;
  UINT            Height;
  UINT            Depth;
} D3DVOLUME_DESC, *LPD3DVOLUME_DESC;
```



## Members

<dl> <dt>

**Format**
</dt> <dd>

Type: **[D3DFORMAT](d3dformat.md)**

</dd> <dd>

Member of the [D3DFORMAT](d3dformat.md) enumerated type, describing the surface format of the volume.

</dd> <dt>

**Type**
</dt> <dd>

Type: **[**D3DRESOURCETYPE**](https://msdn.microsoft.com/en-us/library/Bb172601(v=VS.85).aspx)**

</dd> <dd>

Member of the [**D3DRESOURCETYPE**](https://msdn.microsoft.com/en-us/library/Bb172601(v=VS.85).aspx) enumerated type, identifying this resource as a volume.

</dd> <dt>

**Usage**
</dt> <dd>

Type: **[**DWORD**](https://msdn.microsoft.com/en-us/library/Aa383751(v=VS.85).aspx)**

</dd> <dd>

Currently not used. Always returned as 0.

</dd> <dt>

**Pool**
</dt> <dd>

Type: **[**D3DPOOL**](https://msdn.microsoft.com/en-us/library/Bb172584(v=VS.85).aspx)**

</dd> <dd>

Member of the [**D3DPOOL**](https://msdn.microsoft.com/en-us/library/Bb172584(v=VS.85).aspx) enumerated type, specifying the class of memory allocated for this volume.

</dd> <dt>

**Width**
</dt> <dd>

Type: **[**UINT**](https://msdn.microsoft.com/en-us/library/Aa383751(v=VS.85).aspx)**

</dd> <dd>

Width of the volume, in pixels.

</dd> <dt>

**Height**
</dt> <dd>

Type: **[**UINT**](https://msdn.microsoft.com/en-us/library/Aa383751(v=VS.85).aspx)**

</dd> <dd>

Height of the volume, in pixels.

</dd> <dt>

**Depth**
</dt> <dd>

Type: **[**UINT**](https://msdn.microsoft.com/en-us/library/Aa383751(v=VS.85).aspx)**

</dd> <dd>

Depth of the volume, in pixels.

</dd> </dl>

## Requirements



|                   |                                                                                        |
|-------------------|----------------------------------------------------------------------------------------|
| Header<br/> | <dl> <dt>D3D9Types.h</dt> </dl> |



## See also

<dl> <dt>

[Direct3D Structures](dx9-graphics-reference-d3d-structures.md)
</dt> <dt>

[**GetDesc**](/windows/desktop/api/d3d9helper/nf-d3d9-idirect3dvolume9-getdesc)
</dt> <dt>

[**GetLevelDesc**](/windows/desktop/api/d3d9helper/nf-d3d9-idirect3dvolumetexture9-getleveldesc)
</dt> </dl>

 

 



