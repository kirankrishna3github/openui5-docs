| loio |
| -----|
| e3038209d0e94f4487531956a60ef457 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/e3038209d0e94f4487531956a60ef457.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/e3038209d0e94f4487531956a60ef457) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/e3038209d0e94f4487531956a60ef457)</div>
<!-- loioe3038209d0e94f4487531956a60ef457 -->

## Keyboard Handling

Keyboard handling enables users to access every UI element of the application with the keyboard and is therefore tightly connected to accessibility. Additionally, this aspect is coupled to the screen reader functionality.

***

### General Recommendations

**Accessibility of UI elements**

Make sure that all available features of the application can be accessed by using only the keyboard - *TAB*, arrows, *ENTER* and *SPACE*. The user should be able to activate the functionality of **all** active elements.

> Note:
>    
>   
> Focus and Keyboard Handling<a name="loioe3038209d0e94f4487531956a60ef457__fig_d5m_5pt_zdb"/>
> 
>  ![](loiod365dbb895594bb7a4044d51dca4b445_HiRes.gif "Focus and Keyboard Handling") 
> 
> 

**Tab order and reading order**

The reading order of the page is very important for the application user experience. Those who use keyboard only should be able to navigate easily through every single element. You should always have in mind the fact that the page should have a logical reading order. This is especially important for those who use screen reader software, because in most cases they will follow exactly the tab order of the application and illogical tab orders can confuse them.

> Note:
> When you have to select a country and city from select boxes, the country should be focused first and after that the city.
> 
> 

***

### Tips for Testing

Start the application and put away your mouse.

-   Can you reach every active screen element just by using the keyboard?

    -   Is this true also for dynamically created texts or control elements?

-   Can you navigate within control elements \(for example, list, table, tabstrip\) using arrow keys?

-   Can you also navigate away from each UI element using the keyboard?

-   Does the visible focus follow the exact keyboard commands? Is it always identifiable and in the visible area?

-   Can you execute all actions? \(Compare with what you can do with the mouse\)

