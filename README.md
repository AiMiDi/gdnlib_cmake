


# DGNLIB Source Distribution


Current information on DGNLIB, including detailed API documentation
can be found at:

  http://dgnlib.maptools.org/


## Building


This is a preliminary source distribution, and I have not gone to any
pains to make it easy to configure and build.  To build please do the 
following:

### Unix:

1. Update cpl_config.h to represent your platform accurately.  Generally all
that matters is to #define WORDS_BIGENDIAN on big endian platforms.  The
rest can likely be ignored.<p>

2. Build the programs. 
```
mkdir build
cd build
cmake [-G generator] [-DUSE_SHARED_LIB] ..
```

### Windows:

1. Ensure you have Microsoft Visual C++ 6.x or later installed.

2. Ensure the commandline VC++ environment is setup properly.  You may need
   to run the VCVARS32.BAT script from within the VC++ tree. 

3. Compile the code, and build statically linked executables for the sample
   programs and DLL using the following command.
```
mkdir build
cd build
cmake [-G generator] [-DUSE_SHARED_LIB] ..
```



## Release Notes

### Release 1.11


 o B-Spline support:
   - The DGNT_BSPLINE define was bogus, replaced with DGNT_BSPLINE_POLE.
   - Added support for the following B-Spline related elements:
     o DGNElemBSplineSurfaceHeader (24)
     o DGNElemBSplineCurveHeader (27)
     o DGNElemBSplineSurfaceBoundary (25)
     o DGNElemKnotWeight (26/28)

 o Added initial support for Shared Cell Definition elements

 o 3D solid/surface fixes:
   - Fixed incorrect reading and writing of surftype field.
   - Added boundelms field to DGNElemComplexHeader
   - Added DGNCreateSolidHeaderElem() and DGNCreateSolidHeaderElemFromGroup()
   - Changed DGNCreateComplexHeaderElem() and 
     DGNCreateComplexHeaderElemFromGroup() to only support complex chains/shapes
   - Fixed bug creating solids/surfaces: totlength was 1 word too short.
   - Renamed bogus define DGNSUT_SOLID to DGNSUT_SURFACE_OF_PROJECTION

 o Added support for cloning Cone elements

 o Fixes for uor handling in DGNCreate(). 

 o Treat the most recently read color table as the global color table, 
   instead of just the first one encountered.

 o Added Text Node implementation from Ilya Beylin. 


### Release 1.10


 o Added DGNElemTypeHasDispHdr(), and use it in DGNParseCore() to avoid trying
   to read disp hdr, or attributes from inappropriate elements.

 o Check if a negative amount of attribute information is being read in
   DGNParseCore(), and if so just issue a warning, and skip attempt.

 o Fixed DGNCreateCellHeaderFromGroup() to not pre-transform the bounds.  

 o Fixed missing handling of min/max Z in DGNCreateMultiPointElem(). (Marius)

 o Added surface type to DGNCreateComplexHeaderElem().  (Marius)

 o DGNRad50ToAscii() reimplemented to correct a few problems.  New version
   provided by Armin Berg (iez.com). 

 o Fixes to complex header and cell header creation to set the total group
   size properly, and to set up complex header pad attributes properly.  Now
   passed EDG validation.


### Release 1.9


 o Added DGNLoadTCB(), and fixed problem when writing new elements to an
   existing file without having already read the TCB. 

 o Fixed serious bug in setting the index "offset" location.  Critical for
   writing applications.


### Release 1.8


 o Added support for reading 3D cone (23), 3D surface (18) and 3D solid (19) 
   elements based on contributions from Marius Kintel. 

 o Main site moved to http://dgnlib.maptools.org/


### Release 1.7


 o Improved calcuation of bounding box in DGLCreateTextElem() based on code
   from Matt Kelder. 

 o Added preliminary 3D write support. 

 o Modified DGNCreateTextElem() arguments, and deprecated DGNCreateArcElem2D()
   in favour of DGNCreateArcElem().

 o Report transformation matrix for ViewInfo when dumping.


### Release 1.6


 o Bug fix in DGNGetLinkage() for DMRS recognition from Henk Jan Priester.

 o Added DGNCreateCellHeaderFromGroup() and DGNCreateCellHeaderElem() 
   functions in the write API.

 o Added a Microsoft VC++ makefile (Makefile.vc). 


### Release 1.5


 o Added 2D write support!  

 o Fixed collection of background color in color table (color 255) as per
   bug report by Henk Jan Priester (Justcroft Technical Systems). 

 o Added support for association ids (DGNLT_ASSOC_ID, DGNGetAssocID()). 

 o Fixed problem with updating the DGNInfo.color_table field when a color
   table is read. 

 o Fixed problem with spatial queries either including all of a complex
   element (and it's members) or none. 

 o Added support for reading the eight view descriptions in the TCB element.

 o Added a Makefile in the source distribution.

 o Fixed error with tags in DGNFreeElement() as reported by Henk Jan Priester.



### Release 1.4


 o Added "fast" spatial searching via the DGNSetSpatialFilter() function. 
   This basically just reads the extents information at beginning of 
   geometric features to see if they should be returned. 

 o Actually extract the global origin from the TCB, and use it when 
   transforming points.  Only a few files (ie. Brazos County roads.rds) use
   a non-zero origin.

 o Added experimental multi byte text support from Ason Kang
   (hiska@netian.com). 

 o Add experimental support for 3D files.  Somes 3d elements not supported. 
   3d quaterion for ellipse and arc elements not utilized. 

 o Added preliminary support for reading cell header structures based
   on input from Mike Cane. 

 o Moved a bunch of stuff into dgnread.cpp. 

 o Build default colortable into dgnhelp.cpp for use of DGNLookupColor(). 

 o Added DGNGetShapeFillInfo(). 

 o DGNGetShapeFillInfo() now tries to handle multi-part attribute linkages.


### Release 1.3


 o Added raw_data/raw_bytes members of DGNElemCore, and DGNSetOptions()
   to allow control of when raw element image is retained. 

 o Added -r flag to dgndump to dump raw contents of desired elements. 

 o Add CPL_CVSID() to simplify tracking of versions. 

 o Fixed bug with freeing element index in DGNClose(). 


