<!-- loio9c6400eb7dc145b78e94a81e6e390780 -->

| loio |
| -----|
| 9c6400eb7dc145b78e94a81e6e390780 |

<div id="loio">

view on: [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/9c6400eb7dc145b78e94a81e6e390780) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/9c6400eb7dc145b78e94a81e6e390780)</div>

## Make Your App Performant

In case of performance issues, follow this checklist to see if you can resolve them yourself, or at least provide a pre-analysis when requesting support.

Many performance issues are configuration-related. The configuration of OpenUI5 and/or your application may need to be adjusted to enable available performance features. Please always have a look at the OpenUI5 release notes and at [What's New in OpenUI5](What's_New_in_OpenUI5_99ac68a.md)

Follow this guide for a quick step-by-step performance check for your application:

1.  Use the UI5 Support Assistant to check for known issues: [Support Assistant](Support_Assistant_57ccd7d.md)
2.  Ensure that library preloads and modules are loaded asynchronously: [Use Asynchronous Loading](Use_Asynchronous_Loading_676b636.md)
3.  TBD
4.  Use the `manifest.json` descriptor file instead of the bootstrap to define dependencies: XXXXXXXXX
5.  Load OpenUI5 from the content delivery network network \(CDN\): [Variant for Bootstrapping from Content Delivery Network](Variant_for____________Bootstrapping_from_Content_Delivery_Network_2d3eb2f.md)
6.  Make sure that all required resources are available to avoid 404 errors
7.  Use "manifest first" to load the component
8.  Ensure that library preloads are enabled: XXXXXXXXXXXXXXXXXXXXXXXXXXX
9.  Ensure that application resources are loaded with a component preload: XXXXXXXXXXXXXXXXXXXXXX
10. Ensure the routing is configured to load targets asynchronously
11. Check for slow network requests
12. Migrate `jquery.sap.*` modules to their modularised variants: [Legacy jQuery.sap Replacement](Legacy_jQuery.sap_Replacement_a075ed8.md)
13. Migrate synchronous variants of UI5 factories to asynchronous variants: [Legacy Factories Replacement](Legacy_Factories_Replacement_491bd9c.md)
14. Use the OData V2 model preload: [Manifest Model Preload](Manifest_Model_Preload_26ba6a5.md)
15. Use OData V2 metadata caching: XXXXXXXXXXXXX
16. Check lists and tables: XXXXXXXXXXXXXXXXX
17. Further optimize your code: XXXXXXXX
18. Render pages while waiting for the response of network requests \(reduce idle times\): XXXXXXXXXXXXX
19. Cache XML Preprocessor results: XXXXXXXXXXXXXXXXXXXX

Blog: SAPUI5 Application Startup Performance - Troubleshooting
