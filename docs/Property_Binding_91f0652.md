| loio |
| -----|
| 91f0652b6f4d1014b6dd926db0e91070 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/91f0652b6f4d1014b6dd926db0e91070.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/91f0652b6f4d1014b6dd926db0e91070) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/91f0652b6f4d1014b6dd926db0e91070)</div>
<!-- loio91f0652b6f4d1014b6dd926db0e91070 -->

## Property Binding

With property binding, you can initialize properties of a control automatically and update them based on the data of the model.

To define property binding on a control, you have the following options:

-   As part of the control’s declaration in an XML view

-   Using JavaScript, in the `settings` object in the constructor of a control, or in special cases, using the `bindProperty` method of a control


Once you have defined the property binding, the property is updated automatically every time the property value of the bound model is changed, and vice versa.

Let’s say, we have the following JSON data:

```lang-js
{
		"company" : {
		"name"  : "Acme Inc."
		"street": "23 Franklin St."
		"city"  : "Claremont"
		"state" : "New Hampshire"
		"zip"   : "03301"
		"revenue": "1833990"
	}
}
```

To define property binding in the control declaration in the **XML view**, just include the binding path within curly brackets \(see also [Binding Path](Binding_Path_2888af4.md)\):

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Input
		value="{/company/name}"
	/>
</mvc:View>
```

In **JavaScript**, you can include the binding path within curly brackets as a string literal in the `settings` object:

```lang-js
// "Input" required from module "sap/m/Input"
var oInput = new sap.m.Input({
	value: "{/company/name}"
});
```

You can also use a complex syntax for property bindings. This complex syntax allows you to define additional binding information to be contained in the `settings` object, such as a formatter function.

If you are working with **XML views**, make sure that you've turned on complex binding syntax in your bootstrap script, as shown here:

``` html

<script
       id="sap-ui-bootstrap"
  	src="https://openui5.hana.ondemand.com/resources/sap-ui-core.js"
  	data-sap-ui-theme="sap_belize"
 	*HIGHLIGHT START*data-sap-ui-bindingSyntax="complex"*HIGHLIGHT END*
  	data-sap-ui-async="true"
  	data-sap-ui-onInit="module:sap/ui/sample/main"
       data-sap-ui-resourceRoots='{"sap.ui.sample": "./"}'
></script>
```

You can also use `data-sap-ui-compatVersion="edge"` to enable complex bindings.

You can then set the `bindingMode` or other additional properties like this:

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Input
		value="{
			path:'/company/name', 
			mode: 'sap.ui.model.BindingMode.OneWay' 
		}"
	/>  
</mvc:View>
```

In **JavaScript** views or controllers, you use a JS object instead of a string literal. This must contain a `path` property containing the binding path, and can contain additional properties:

```lang-js
// "Input" required from module "sap/m/Input"
// "BindingMode" reqzured from module "sap/ui/model/BindingMode"

var oInput = new Input ({
    value: {
		path: "/company/name",
		mode: BindingMode.OneWay
	}
});
```

Depending on the use case, it may be useful to define the binding at a later time, using the `bindProperty` method:

```lang-js
oInput.bindProperty("value", "/company/name");
```

This option also allows you to use the same object literal that you used in the constructor to define the binding:

```lang-js
// "TypeInteger" required from module "sap/ui/model/type/Integer"

oInput.bindProperty("value", {
	path: "/company/name",
	type: new TypeInteger()
});
```

> Note:
> Some controls offer convenience methods for their main properties that are most likely to be bound by an application:
> 
> ```lang-js
> oTextField.bindValue("/company/name");
> ```
> 
> 

To **remove** a property binding, you can use the `unbindProperty` method. The property binding is removed automatically whenever a control is destroyed:

```lang-js
oTextField.unbindProperty("value");
```

***

<a name="loio91f0652b6f4d1014b6dd926db0e91070__section_N10078_N10013_N10001"/>

### Formatting Property Values

Values in data are often represented in an internal format and need to be converted to an external format for visual representation, especially numbers, dates, and times with locale-dependent external formats. OpenUI5 provides two different options for converting data. You can use both options for each binding, you don't have to use one option consistently throughout your app:

-   Formatter functions for one-way conversion

-   Data types in two-way binding

    Data types can be used to parse user input in addition to formatting values.


***

#### Using a Formatter Function

If you define the property binding in the **XML view**, you need to define a formatter function \(`roundToMillion`\) in the view controller:

```lang-js
sap.ui.define([
	"sap/ui/core/mvc/Controller",
	"sap/ui/model/json/JSONModel"
], function (Controller, JSONModel) {
	"use strict";
	return Controller.extend("sap.ui.sample.App", {
		……………
		roundToMillion: function(fValue) {
			if (fValue) {
				return "> " + Math.floor(fValue/1000000) + "M";
			}
			return "0";
		}
	});
}); 
```

The `this` context of a formatter function is generally set to the control \(or managed object\) that owns the binding. However, in XML views, the reference to the formatter is done in the view controller by putting a dot \(`.`\) in front of the name of the formatter function \(`{ formatter: '.myformatter' }`\). In this case, the formatter's `this` context is bound to the controller.

``` xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Input
		value="{ path:'/company/revenue',
		formatter: '*HIGHLIGHT START*.*HIGHLIGHT END*roundToMillion'}"
	/>
</mvc:View>
```

If you use **JavaScript**, you can pass the formatter function as a third parameter to the `bindProperty` method, or you can add the binding info with the `formatter` key. The `formatter` has a single parameter `value`, which is the value that is to be formatted, and is executed as a member of the control, meaning it can access additional control properties or model data.

```lang-js
//"Input" required from module sap/m/Input

oTextField.bindProperty("value", "/company/title", function(sValue) {
	return sValue && sValue.toUpperCase();
});

oControl = new Input({
	value: {
		path:"/company/revenue",
		formatter: function(fValue) {
			if (fValue) {
				return "> " + Math.floor(fValue/1000000) + "M";
			}
			return "0";
		}
	}
})
```

Because it can contain any JavaScript, the formatter function can be used for formatting a value and also for performing type conversions or calculating results, for example, to show a special traffic light image depending on a Boolean value:

```lang-js
oImage.bindProperty("src", "/company/trusted", function(bValue) {
	return bValue ? "green.png" : "red.png";
}); 
```

> Note:
> The framework only updates a binding when one of the properties included in the binding changes. If the formatter uses another property value that is not part of the binding definition, the framework won't know that the result depends on that additional property and could miss necessary updates. Therefore, make sure that you declare a composite binding referencing all necessary properties \(maybe even from different models\).
> 
> 

***

#### Using Data Types

The data type system enables you to format and parse data, as well as to validate whether the entered data lies within any defined constraints. OpenUI5 comes with several predefined and ready-to-use types, referred to as simple types. For more information, see [Formatting, Parsing, and Validating Data](Formatting,_Parsing,_and_Validating_Data_07e4b92.md).

Here’s how you can use these types in an XML view:

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Input
		value="{ path:'/company/revenue',
		type: 'sap.ui.model.type.Integer'}"/>
</mvc:View>

```

You can also provide parameter values for some of the simple types in your XML view. These are declared as `formatOptions`, as you can see in the Float type sample below. Permitted `formatOptions` are properties of the corresponding data type. For more information, see the *API Reference* in the Demo Kit.

```lang-xml
<mvc:View
   controllerName="sap.ui.sample.App"
   xmlns="sap.m"
   xmlns:mvc="sap.ui.core.mvc">
   <Input
      value="{ path:'/company/revenue', 
           type: 'sap.ui.model.type.Float',
           formatOptions: {
                   minFractionDigits: 2,
                   maxFractionDigits: 2
           }
      }"/>
</mvc:View>
```

Using JavaScript, you can define a type to be used for a property binding by passing it as a third parameter in `bindProperty` or by adding it to the binding information by using the key `type`, as shown here:

```lang-js
// "TypeString" required from module "sap/ui/model/type/String"
// "Input" required from module "sap/m/Input"
// "TypeFloat" required from module "sap/ui/model/type/Float"

oTextField.bindProperty("value", "/company/name", new sap.ui.model.type.String());

oControl = new sap.m.Input({
    value: {
        path:"/company/revenue",
        type: new TypeFloat({
            minFractionDigits: 2,
            maxFractionDigits: 2
        })
    }
})
```

Predefined data types also offer visual feedback for erroneous user input. To turn this feature on, add the following line to your controller's `init` function:

```lang-js
sap.ui.getCore().getMessageManager().registerObject(this.getView(), true);
```

You can define **custom types** by inheriting from `sap.ui.model.SimpleType` and implementing the three methods `formatValue`, `parseValue`, and `validateValue`. `formatValue` is called whenever the value in the model is changed to convert it to the type of the control property it is bound to, and may throw a `FormatException`. `parseValue` is called whenever the user has modified a value in the UI and the change is transported back into the model. It may throw a `ParseException` if the value cannot be converted. If parsing is successful, `validateValue` is called to check additional constraints, such as minimum or maximum value, and throws a `ValidateException` if any constraints are violated.

```lang-js
// "SimpleType" required from module "sap/ui/model/SimpleType"
// "ValidateException" required from module "sap/ui/model/ValidateException"

var Zipcode = SimpleType.extend("sap.ui.sample.Zipcode", {
    formatValue: function(oValue) {
        return oValue;
    },
    parseValue: function(oValue) {
        return oValue;
    },
    validateValue: function(oValue) {
       if (!/^(\d{5})?$/.test(oValue)) {
            throw new ValidateException("Zip code must have 5 digits!");
       }
    }
});
```

You can use your custom types in XML views or JavaScript in the same way as you would apply predefined types:

```lang-xml
<mvc:View
   controllerName="sap.ui.sample.App"
   xmlns="sap.m"
   xmlns:mvc="sap.ui.core.mvc">
   
   <Input
      value="{ path:'/company/zip',
      type: 'sap.ui.sample.Zipcode'
     }"/>

</mvc:View>
```

***

<a name="loio91f0652b6f4d1014b6dd926db0e91070__section_N100DE_N10013_N10001"/>

### Changing the Binding Mode

By default, all bindings of a model instance have the default binding mode of the model, but you can change this behavior if needed. When creating a `PropertyBinding`, you can specify a different binding mode, which is then used exclusively for this specific binding. Of course, a binding can only have a binding mode that is supported by the model in question.

```lang-js
// "JSONModel" required from module "sap/ui/model/json/JSONModel"
// "Input" required from module "sap/m/Input"
// "BindingMode" required from module "sap/ui/model/BindingMode"
	var oModel = new JSONModel();
	// default binding mode is two way
	oModel.setData(myData);
	sap.ui.getCore().setModel(oModel);
	var oInputFirstName = new Input ();
	
	// bind value property one way only
	// propertyname, formatter function, binding mode
	oInputFirstName.bindValue("/firstName", null, BindingMode.OneWay);
	oInputFirstName.placeAt("target1");

	oInputLastName = new Input();
	// bind value property two way (default)
	oInputLastName.bindValue("/lastName");
	oInputLastName.placeAt("target2");
```

In the example above, two `Input` fields are created and their `value` property is bound to the same property in the model. The first `Input` binding has a one-way binding mode, whereas the second `Input` has the default binding mode of the model instance, which is two-way. For this reason, when text is entered in the first `Input`, the value will **not** be changed in the model. This only happens if text is entered in the second `Input`. Then, of course, the value of the first `Input` will be updated as it has a one-way binding, that is, from model to view.

**Related information**  


[Data Binding Tutorial Step 3: Create Property Binding](Step_3_Create_Property_Binding_d70e989.md)

[API Reference: `sap.ui.base.ManagedObject.bindProperty`](https://openui5.hana.ondemand.com/#/api/sap.ui.base.ManagedObject/methods/bindProperty)

[Binding Syntax](Binding_Syntax_e2e6f41.md)

[Formatting, Parsing, and Validating Data](Formatting,_Parsing,_and_Validating_Data_07e4b92.md)
