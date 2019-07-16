| loio |
| -----|
| f51dbb78e7d5448e838cdc04bdf65403 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/f51dbb78e7d5448e838cdc04bdf65403.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/f51dbb78e7d5448e838cdc04bdf65403) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/f51dbb78e7d5448e838cdc04bdf65403)</div>
<!-- loiof51dbb78e7d5448e838cdc04bdf65403 -->

## Stable IDs: All You Need to Know

Stable IDs are IDs for controls, elements, or components that you set yourself in the respective `id` property or attribute as opposed to IDs that are generated by OpenUI5. *Stable* means that the IDs are concatenated with the application component ID and do not have any auto-generated parts.

***

<a name="loiof51dbb78e7d5448e838cdc04bdf65403__section_gtm_xlp_3z"/>

### Background

If you don't define IDs, OpenUI5 generates them dynamically. These IDs are not static and might differ from program run to program run. For example, the page and table in the following XML view could have the generated IDs `__page0` and `__table0` at runtime:

```lang-xml
<mvc:View
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Page>
		<content>
			<Table>
			</Table>
		</content>
	</Page>
</mvc:View>

```

The generated IDs change whenever the control structure of the app changes. The sequence of instantiation also plays a role: If there are two views with unstable IDs in the app, depending on the order the views are opened, they get the generated IDs `__view0` and `__view1`. This is an issue for the following features that require stable IDs:

-   SAPUI5 flexibility

    Allows you to adapt apps based on your requirements, for example, by creating variants or changing the user interface at runtime. Stable IDs are used to identify the controls that are to be adapted.

-   Automated tests

    To check the behavior of apps at runtime, these tests find controls by searching for stable IDs. If you use OPA in OpenUI5, you're able to find controls via other criteria like control type, display name and others. For more information, see [Integration Testing with One Page Acceptance Tests \(OPA5\)](Integration_Testing_with_One_Page_Acceptance_Tests_(OPA5)_2696ab5.md).

-   Inline help tools

    These tools display user assistance information directly in the app and depend on stable IDs \(example: Web Assistant\).


> Note:
> Stable IDs are an important prerequisite for SAPUI5 flexibility services, automated testing, and inline help tools, such as Web Assistant. Apps with stable IDs are of high quality and offer customers more functionality. Therefore, we strongly recommend that you use stable IDs whenever possible \(some technical controls don't need stable IDs, such as `CustomData`\).
> 
> 

***

<a name="loiof51dbb78e7d5448e838cdc04bdf65403__section_fc4_4w5_1bb"/>

### Here's how you set IDs manually to keep them stable

|**Views**| -   Views in the descriptor for applications, components, and libraries

The standard use case is that you use stable IDs for the view that the router navigates to. Ideally, instead of creating the views yourself, you create them with routing targets and declare the view ID in the manifest.json file as shown in the example below. For more information, see [Routing and Navigation](Routing_and_Navigation_3d18f20.md) and [Descriptor for Applications, Components, and Libraries](Descriptor_for_Applications,_Components,_and_Libraries_be0cf40.md).

Example:

    ```lang-js
{
"sap.ui5": {
	"rootView": {
		"viewName": "<your namespace>.view.Root",
		"id" : "rootView",
		"async": true,
		"type": "XML"
	}
	...
	"routing": {
		...
		"targets": {
			"myTarget": {
				"viewName": "MyView",
				"viewId": "myView"
				}
			}
		}
	}
}

    ```

-   Embedded views

If you embed your view, set its ID \(such as `myEmbeddedView`\).

Example:

    ```lang-xml
<mvc:View xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Page id="page">
		<mvc:XMLView id="myEmbeddedView" viewName="MyView" async="true" />
	</Page>
</mvc:View>

    ```

-   Programmatic creation

If you create the view programmatically, provide the ID as one of the parameters to the constructor or factory function. Make sure to prefix the view ID with the component ID using the `createId` method of the owner component.

Example:

    ```lang-js
// "XMLView" required from module "sap/ui/core/mvc/XMLView"
XMLView.create({
	id: <component>.createId("myProgrammaticView"),
	viewName : "<your namespace>.view.ProgrammaticView"
}).then(function(oView){
	// code
});

    ```

For more information, see [namespace sap.ui](https://openui5.hana.ondemand.com/#/api/sap.ui/methods/view).


 |
 > **Warning:** The below table contains complex elements that cannot not be displayed within a simple markdown table. It has been automatically converted to an HTML table. It's design may vary from the source page!

<table>
	<thead>
		<tr>
			<th> **Extension points** </th>
			<th>If you use extension points, use stable IDs for nested views and prefixes for nested controls of a fragment.</th>
		</tr>
	</thead>
	<tbody>

The XML view prefixes the control IDs \(only the defined IDs, not the automatically created ones\) with its own ID. This allows you to use the same control ID for different views and the same view multiple times. For more information, see [Support for Unique IDs](Support_for_Unique_IDs_91f28be.md).

If the following XML view is instantiated using the ID `myView`, the contained page and table would have the IDs `myView--page` and `myView--table` at runtime:

    ```lang-js
<mvc:View xmlns="sap.m" xmlns:mvc="sap.ui.core.mvc">
	<Page id="page">
		<content>
			<Table id="table">
			</Table>
		</content>
	</Page>
</mvc:View>

    ```

 -   Programmatic creation

For JavaScript views and JavaScript-generated controls you must use the `createID` method of the view or component. Here's how it could look like when you're creating a control directly in the control code:

    ```lang-xml
// "Button" required from module "sap/m/Button"
new Button({
	id : oView.createId("ConfirmButton"),
	text : "Confirm"
});
    ```
			</td>
		</tr>
		<tr>
			<td> **Components** </td>
			<td>

 > Note:
 > The following is only relevant if you do not use the SAP Fiori launchpad because it instantiates components for you and provides IDs.

 For example, if you instantiate a component inside an HTML page, set the ID of the component as shown below. The reason for this is that components could be displayed more than once on a page. To get unique IDs for the views and controls inside the component, they must be prefixed with the component ID. All views in the component that are created by the framework are automatically prefixed with the component ID. As described above, for the programmatically generated components, you must do it yourself. Example: ```lang-js
// "Shell" required from module "sap/m/Shell"
new Shell({
```

> Note:
> Only if there's more than one component in an app, the component container requires a stable ID by setting the component container to `autoPrefixId`. For more information, see [sap.ui.core.ComponentContainer](https://openui5.hana.ondemand.com/#docs/api/symbols/sap.ui.core.ComponentContainer.html).
> 
> 

 |
| *HIGHLIGHT START*Embedded Components*HIGHLIGHT END* |If you want to add an embedded component with a stable ID, you have to add a component re-use entry in the application component's manifest.json. Let's say you want to add an embedded component with the name `embeddedComponent.name`. You define it as follows in the application component's manifest.json file: ```lang-json
"sap.ui5": {
   "componentUsages": {
      "reuseName": {
         "name": "embeddedComponent.name",
         "settings": {
            "id": "embeddedComponentID"
         }
      }
   }
}

```
   "componentUsages": {
      "reuseName": {
         "name": "embeddedComponent.name",
         "settings": {
            "id": "embeddedComponentID"
         }
      }
   }
}
```

 > Note:
> In order to support SAPUI5 flexibility features, all embedded components should have a stable ID.
> 
> 

 |
| *HIGHLIGHT START*XML fragments*HIGHLIGHT END* |If you are using XML fragments in your app, make sure they are instantiated using the correct view ID prefix. Example: ```lang-js
// "Fragment" required from module "sap/ui/core/Fragment"
Fragment.load({
	id: this.getView().getId(),
	name: "my.fragment.SampleFragment"
});
```
			</td>
		</tr>
		<tr>
			<td> **XML fragments** </td>
			<td>If you are using XML fragments in your app, make sure they are instantiated using the correct view ID prefix. Example: 

```
lang-js// "Fragment" required from module "sap/ui/core/Fragment"
Fragment.load({
	id: this.getView().getId(),
	name: "my.fragment.SampleFragment"
});
```
			</td>
		</tr>
	</tbody>
</table>
> Note:
> If some controls have disappeared after a software upgrade or the way in which they can be identified has been changed, this has a direct impact on the functions that depend on stable IDs. For this reason, the IDs, which are part of the public API of the app, must be kept stable over the life cycle of the app.
> 
> 

***

<a name="loiof51dbb78e7d5448e838cdc04bdf65403__section_lvk_cqp_3z"/>

### How to name stable IDs

Choose names for your stable IDs that describe the semantics of your views and controls, such as *page* or *table*.

> Note:
> For the allowed sequence of characters, see the [namespace sap.ui.core.ID](https://openui5.hana.ondemand.com/#docs/api/symbols/sap.ui.core.ID.html). But bear in mind not use hyphens \(-\) as separators in your names as they would interfere with the ones that are added automatically by the framework.
> 
> 

Example:

If you build an app using the following stable IDs for the component and the views using the SAP Fiori Worklist Application template, here's what the concatenated IDs that are generated at runtime look like:

|Component|Views|Contained views|Concatenated IDs|
|---------|-----|---------------|----------------|
| `myProducts` | `worklist` | `page` | `myProducts---worklist--page` |
| `table` | `myProducts---worklist--table` |
| `product` | `page` | `myProducts---product--page` |
| `objectHeader` | `myProducts---product--objectHeader` |

For more information about the SAP Fiori Worklist Application template, see [Worklist Template](Worklist_Template_a77f2d2.md).
