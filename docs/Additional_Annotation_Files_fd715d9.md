| loio |
| -----|
| fd715d97ebf842739697c9a0f276f0c0 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/fd715d97ebf842739697c9a0f276f0c0.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/fd715d97ebf842739697c9a0f276f0c0) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/fd715d97ebf842739697c9a0f276f0c0)</div>
<!-- loiofd715d97ebf842739697c9a0f276f0c0 -->

## Additional Annotation Files

The OData V4 model supports loading of additional annotation files.

The annotation files have to be given during creation of an `ODataModel` instance. Adding annotation files at a later point in time is **not** supported.

The format of the annotation file has to be the same as the metadata file of the service. Only XML files are supported. You can specify the annotation files in the descriptor for applications, components, and libraries \(`manifest.json`\).

Annotation files are specified in `manifest.json` as follows:

```lang-js

"dataSources" : {
    "default" : {
        "uri" : "/sap/opu/odata4/IWBEP/V4_SAMPLE/default/IWBEP/V4_GW_SAMPLE_BASIC/0001/",
        "type" : "OData",
        "settings" : {
            "annotations": ["localAnnotations"],
            "odataVersion" : "4.0"
        }
    },
    "localAnnotations": {
        "uri": "data/annotations.xml",
        "type": "ODataAnnotation"
    }
},
```

Annotation files are usually defined as data sources in `manifest.json`. In the example above, the annotation file is located relative to the component. In the `dataSource` definition of the OData service, you can reference these annotation data sources in the `annotations` setting. The content of the annotation files are then merged into the service metadata in the given order \(the last one wins\). Every \(target, term, qualifier\)-tuple must appear at most once within `$metadata` documents, but can be overwritten by annotation files.

Annotation terms are not merged, but replaced as a whole \(“PUT” semantics\). For example, if you have defined the sort restriction annotation `Org.OData.Capabilities.V1.SortRestrictions` at the `BusinessPartnerSet` as shown in the example below, you have to repeat the term in your annotation file if you want to add, for example, the additional property `AscendingOnlyProperties`.

The annotation term is specified in the service metadata document:

```lang-js

<Annotations Target="GWSAMPLE_BASIC.GWSAMPLE_BASIC_Entities/BusinessPartnerSet">
    <Annotation Term="Org.OData.Capabilities.V1.SortRestrictions">
        <Record>
            <PropertyValue Property="NonSortableProperties">
                <Collection>
                    <PropertyPath>BusinessPartnerID</PropertyPath>
                </Collection>
            </PropertyValue>
        </Record>
    </Annotation>
</Annotations>
```

If an additional property needs to be added, the term has to be repeated in the annotation file:

```lang-js

<Annotations Target="GWSAMPLE_BASIC.GWSAMPLE_BASIC_Entities/BusinessPartnerSet">
    <Annotation Term="Org.OData.Capabilities.V1.SortRestrictions">
        <Record>
            <PropertyValue Property="AscendingOnlyProperties">
                <Collection>
                    <PropertyPath>AnyPropertyPath</PropertyPath>
                </Collection>
            </PropertyValue>
            <PropertyValue Property="NonSortableProperties">
                <Collection>
                    <PropertyPath>BusinessPartnerID</PropertyPath>
                </Collection>
            </PropertyValue>
        </Record>
    </Annotation>
</Annotations>
```
