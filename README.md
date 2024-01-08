[threejs-ifc-export](https://dirkarnez.github.io/threejs-ifc-export/)
=====================================================================
### Code
```ts

    interface pt {
        x: number, y: number, z: number;
    }

    const gridSize = 6;

    let dir: pt =  { x: 0, y: 0, z: 1 };
    let rad: number = 0.25;
    let len: number = 2;
    let direction = ifcAPI.CreateIfcEntity(model,IFCDIRECTION, [ifcAPI.CreateIfcType(model,IFCREAL,dir.x), ifcAPI.CreateIfcType(model,IFCREAL,dir.y), ifcAPI.CreateIfcType(model,IFCREAL,dir.z)]);
    let profileLocation = ifcAPI.CreateIfcEntity(model,IFCCARTESIANPOINT, [ifcAPI.CreateIfcType(model,IFCLENGTHMEASURE,0), ifcAPI.CreateIfcType(model,IFCLENGTHMEASURE,0)]);
    let profileAxis = ifcAPI.CreateIfcEntity(model,IFCAXIS2PLACEMENT2D, profileLocation, null);
    let profile =  ifcAPI.CreateIfcEntity(model, IFCCIRCLEPROFILEDEF, IFC4.IfcProfileTypeEnum.AREA, ifcAPI.CreateIfcType(model,IFCLABEL,'column-prefab'), profileAxis, ifcAPI.CreateIfcType(model,IFCPOSITIVELENGTHMEASURE,rad));   

    for (let i = 0; i < gridSize; i++) {
        for (let j = 0; j < gridSize; j++) {
        
            let pos:pt = {x: i, y: j, z: 0};
       

            let location = ifcAPI.CreateIfcEntity(model,IFCCARTESIANPOINT, [ifcAPI.CreateIfcType(model,IFCLENGTHMEASURE,pos.x), ifcAPI.CreateIfcType(model,IFCLENGTHMEASURE,pos.y),ifcAPI.CreateIfcType(model,IFCLENGTHMEASURE,pos.z)]);
            let placement= ifcAPI.CreateIfcEntity(model, IFCAXIS2PLACEMENT3D, location, null, null);
            

            let solid = ifcAPI.CreateIfcEntity(model, IFCEXTRUDEDAREASOLID, profile, placement, direction, ifcAPI.CreateIfcType(model,IFCPOSITIVELENGTHMEASURE,len));

            let column = ifcAPI.CreateIfcEntity(model,IFCCOLUMN, ifcAPI.CreateIfcType(model, IFCGLOBALLYUNIQUEID,"GUID"), null,ifcAPI.CreateIfcType(model,IFCLABEL,"name"),null, ifcAPI.CreateIfcType(model,IFCLABEL,"label"),  placement, solid,ifcAPI.CreateIfcType(model,IFCIDENTIFIER,"sadf"), null);

            ifcAPI.WriteLine(model, column);
        }

    }


var filename = "test.ifc";
const a = ifcAPI.ExportFileAsIFC(filename, model, {
  coordinationView: "IFC4RV",
  ifcSchemaVersion: "IFC4_ADD2_TC1",
  useStandardizedNames: false
});

var s = new TextDecoder().decode(a);
debugger;
```

**https://github.com/IfcOpenShell/IfcOpenShell/blob/v0.7.0/src/blenderbim/scripts/obj2ifc.py**
### Tools
- `.ifc`
  - https://ifcjs.github.io/web-ifc/demo/
  - https://ifcjs.github.io/web-ifc-three/example/index
  - https://ifcjs.github.io/web-ifc-viewer/example/index
- `.obj`
  - [Online 3D Viewer](https://fetchcfd.com/3d-viewer)
  - [Creators 3D | Online 3D Viewer](https://www.creators3d.com/online-viewer)
  - [Online 3D Viewer](https://3dviewer.net/)
  - [Free 3D Viewer Online, open and share models - 3D Viewer Max](https://3dviewermax.com/)
### TODOs
- [ ] obj generation -> geometry extraction
- [ ] **https://github.com/IfcOpenShell/IfcOpenShell/blob/v0.7.0/src/blenderbim/scripts/obj2ifc.py**
- [ ] Simplify ifc input (primitive shape fitting / primitive decomposition)
 - > 3D Reconstruction Software: Some 3D reconstruction software packages, like MeshLab or CloudCompare, offer features for primitive shape fitting. These tools often provide automated algorithms or interactive tools to decompose complex objects into simpler shapes.
### Format
- https://standards.buildingsmart.org/IFC/DEV/IFC4_2/FINAL/HTML/annex/annex-e/brep-model.ifc.htm
- https://standards.buildingsmart.org/IFC/DEV/IFC4_2/FINAL/HTML/annex/annex-e/basin-faceted-brep.ifc
- https://standards.buildingsmart.org/IFC/DEV/IFC4_2/FINAL/HTML/annex/annex-e/brep-model.htm

