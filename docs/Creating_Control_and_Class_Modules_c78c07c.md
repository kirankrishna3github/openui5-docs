| loio |
| -----|
| c78c07c094e04ccfaab659378a1707c7 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/c78c07c094e04ccfaab659378a1707c7.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/c78c07c094e04ccfaab659378a1707c7) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/c78c07c094e04ccfaab659378a1707c7)</div>
<!-- loioc78c07c094e04ccfaab659378a1707c7 -->

## Creating Control and Class Modules

Modules do not only require and use functionality from other modules, they also expose their own functionality to the outside. In asynchronous module definition \(AMD\) syntax, there are several ways to expose such functionality.

However, OpenUI5 only supports the "module return value".

If you want to export the "module value" of an AMD module under a global name, you have two options:

-   You rely on the OpenUI5 methods that already do the exposure as a side effect, such as:
    -   Classes created by the `extend` method

    -   Libraries that call `initLibrary()` in their `library.js` module

    -   Renderers that are created with `sap.ui.core.Renderer.extend(“….”)`

-   You set the fourth parameter `bExport of sap.ui.define(sModuleName, aDependencies, vFactory, bExport)` to `true`. This will expose the module value under the global name that is derived from the module name.

    The global JavaScript namespace is based on a "slash to dot replacement".

    > Note:
    > The resulting namespace might not have the expected result if the AMD module name contains dots!
    > 
    > 


In control and class modules, you should not use global variables at all. When you derive a custom control from an existing superclass via the the `extend` method, the resulting subclass is returned.

You can store the return value of the extend function in a local variable, make changes to the prototype and then return this variable as the modules return value.

JSDoc for the class should use the `@alias` tag to make sure that the variable is known under the global name in the generated JSDoc.

The `extend` function makes sure that the respective namespace is created:

```lang-js
sap.ui.define(["sap/ui/base/Object", "sap/ui/model/json/JSONModel"], function (BaseObject, JSONModel) {
  
    var Foo = BaseObject.extend("foo.bar.MyClass", /** @lends foo.bar.MyClass */ {
  
      constructor: function(sId, mProperties) {
        this.mId = sId;
      }
    });
 
    Foo.prototype.ownMethod = function (a) {
        return a * 2;
    };
  
    // return the module value, in this example a class
    return Foo;
});
```

**Related information**  


[Example for Defining a Class](Example_for_Defining_a_Class_f6fba4c.md)
