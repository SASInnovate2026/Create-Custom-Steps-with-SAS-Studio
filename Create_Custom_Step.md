# Create Custom Steps with SAS Studio
* [Exercise Description](#exercise-description)
* [Log in to SAS Viya](#log-in-to-sas-viya)
* [Create a Custom Step](#create-a-custom-step)
  * [*Assignment*: Complete Page 1 UI](#assignment-complete-page-1-ui)
  * [Set Port Details](#set-port-details)
  * [*Assignment*: Build Page 2 UI](#assignment-build-page-2-ui)
  * [*Assignment*: Build Page 3 UI](#assignment-build-page-3-ui)
  * [Add Code to the Custom Step](#add-code-to-the-custom-step)
* [Open and Test the Custom Step in Stand-Alone Mode](#open-and-test-the-custom-step-in-stand-alone-mode)
  * [Assignment: Test the Custom Step](#assignment-test-the-custom-step)
* [Use the Custom Step in a SAS Studio Flow](#use-the-custom-step-in-a-sas-studio-flow)
* [Exercise Completed](#exercise-completed)

<br>

## Exercise Description
In this hands-on exercise you create a custom step that calculates the geo-distance between two latitude and longitude locations in either kilometers or miles and provide the option to round the result.  After the custom step is built, you test it in stand-alone mode and then use it in a SAS Studio Flow.

<br>
<br>

## Log in to SAS Viya
Open a new window in the *Google Chrome* browser and select the **SASLanding** bookmark.

* ID: **student**
* Password: **Metadata0**

Select **No** when prompted about accepting *Admin* privileges.

<br>

## Create a Custom Step
1. Select ![Viya Menu Selector](images/HamburgerMenu.png) **&#10132; Develop Code and Flows** to open *SAS Studio*.
1. Select ![Steps Pane](images/Steps.png) to view the **Steps** pane.
1. Select ![New](images/New.png) &#10132; **Custom step quick start** to create a new custom step.
1. On the **Properties** for the *Page* on the *Design* tab, enter the following:
   - ID: **GeoDist**
   - Label: **Calculate Geo Distance**

     ![Custom Step Page 1](images/CSPage1.png)

1. Drag the **Input Table** *Data* control onto the canvas.
1. Enter the **Properties** for the *Input Table*, enter the following:
   - ID: **inTable**
   - Label: **Input table**
   - ![Selected Checkbox](images/SelectedCheckbox.png) Required

    > &#8252; The **ID** names for the controls are used in the code for the custom step, so ensure you enter them correctly; otherwise, you will either need to edit the code or the control ID.

   ![Custom Step Input Table](images/CSInputTable.png)

1. Select ![Save](images/Save.png) to save the custom step.
1. Navigate to **SAS Content &#10132; Public**.
1. Enter **GeoDistance with Rounding** for the *name* and click **Save**.
1. Select the **Custom Steps** tab and confirm the saved step is listed there.

    ![](images/CSSaveStep.png)

<br>
<br>

### *Assignment*: Complete Page 1 UI
Add a **Radio Button Group** *Common* control to the canvas.  Enter the properties as depicted below.

   > &#9755; Click ![Radio Button Add Item](images/CSAddItem.png) to add an item to the radio button list.

![Custom Step Distance Type Radio Button](images/CSdisType.png)

<br>

Add a **Section** *Common* control to the canvas.  Enter the properties as depicted below.

![Custom Step Section Control](images/CSSection.png)

<br>

**Save** the changes to the custom step.

<br>

Add a **Column Selector** *Data* control to the canvas in the *Lat/Long Columns* section group.  Enter the properties as depicted below.

   > &#9755; Right-click the control once added to the canvas and select **Move to section &#10132; Lat/Long Columns** to place it in the section.

![Custom Step Column Selector 1](images/CSLoc1.png)

<br>

**Duplicate** the *Location1 Column Selector* control and paste it below in the *Lat/Long Columns* section group.  Edit the properties as depicted below.

   > &#9755; Right-click the *Location 1* control once added to the canvas and select **Duplicate**.

![Custom Step Column Selector 2](images/CSLoc2.png)

<br>

**Save** the changes to the custom step.

<br>

Add a **New Column** *Data* control to the main canvas.  Enter the properties as depicted below.

![New Column Control](images/NewColumnControl.png)

  > &#9998; Setting visibility to *false* means that the user will not be able to view this control.  The column name will be controlled by the code, but is needed for the output options in the port details you will set later in this exercise.

<br>

Add an **Output Table** *Data* control to the main canvas.  Enter the properties as depicted below.

![Custom Step Output Table](images/CSOutTable.png)

<br>

**Save** the Custom Step.  Click **Launch** to preview the design of Page 1 - *Calculate Geo Distance*.

![Custom Step Preview](images/CSPreview.png)

> &#9998; The *new column* is not displayed in the Preview since its visibility is set to *false*.

**Close** the launched custom step when done.

<br>
<br>

### Set Port Details
1. Select ![Port Details](images/PortDetails.png) to enter the port details for the custom step.
1. Select ![](images/PencilIcon.png) for the **outTable** *Output Tables* port to edit its details.

    ![](images/PortDetailsTab.png)

1. Select **All columns &#10132; Input table (inTable)** to add all the columns from that input table to the output.

    ![Add Input Columns](images/AddInputColumnstoOutput.png)

1. Select **New column &#10132; Distance between the locations (newColumn)** to add that new column to the output.

    ![Add Output Columns](images/OutputTableColumns.png)

1. Click **OK** to save the changes to output table metadata.
1. **Save** the changes to the custom step.

<br>
<br>

### *Assignment*: Build Page 2 UI
Create a second page for the custom step by selecting ![Add Page button](images/AddPage.png) in the *Control Library* on the *Designer* tab. Enter the properties as depicted below.

![Custom Step Page 2](images/CSPage2.png)

<br>

**Save** the custom step.

<br>

Add a **Check Box** *Common* control to the canvas on *Page2*.  Enter the properties as depicted below.

![Custom Step Round Check Box](images/CSRound.png)

<br>

**Save** the custom step.

<br>

Add a **Text or Numeric Field** *Common* control to the canvas.  Enter the properties as depicted below.

  > &#9998; **"$round"** in the *Dependencies Visibility* section indicates that this control is dependent on the **round** *Check Box* control and will only be displayed if it is checked.

![Custom Step Num Decimal Places](images/CSDecimalPlaces.png)

<br>

**Save** the custom step.  Select **Launch** to preview Page 2 - *Options* of the custom step.

Confirm that the dependent **decimalPlaces** selection is only displayed if the **round** check box is checked.

**Round Option Unchecked**

  ![Custom Step Option Unchecked](images/CSUnchecked.png)

**Round Option Checked**

  ![Custom Step Option Checked](images/CSChecked.png)

**Close** the launched custom step when done.

<br>
<br>

### *Assignment*: Build Page 3 UI
Add an **About** page (tab).  On the *About* tab, use the **Text** control in the *Common* section to add the following text:
**This custom step calculates the distance between two locations.**

**Save** the custom step.

![About Tab](images/CSAboutTab.png)

<br>
<br>

### Add Code to the Custom Step
1. Select the **Program** tab on the custom step.
1. Copy and Paste the following code:

```sas
/* Set Input and Output Data */
data &outTable ;
	set &inTable ;


/* newColumn is a hidden control in the UI.  The code sets the name of the new output column. */

/* Calculate GeoDistance in Miles */
%if &disType=Miles %then %do ;
	%let newColumn_name=distance_in_Miles ;
	&newColumn_name=geodist(&loc1_1_name, &loc1_2_name, &loc2_1_name, &loc2_2_name, 'M') ;
%end;

/* Calculate GeoDistance in Kilometers */
%else %do ;
	%let newColumn_name=distance_in_Kilometers ;
	&newColumn_name=geodist(&loc1_1_name, &loc1_2_name, &loc2_1_name, &loc2_2_name, 'K') ;
%end ;


/* Round GeoDistance Value */
%if &round=1 %then %do ;
	select(&decimalPlaces) ;
		when(0)  &newColumn_name=round(distance_in_&disType) ;
    	when(1)  &newColumn_name=round(distance_in_&disType,0.1) ;
		when(2)  &newColumn_name=round(distance_in_&disType,0.01) ;
		when(3)  &newColumn_name=round(distance_in_&disType,0.001) ;
		when(4)  &newColumn_name=round(distance_in_&disType,0.0001) ;
		when(5)  &newColumn_name=round(distance_in_&disType,0.00001) ;
    end;
%end;
run;
```

  > &#8252; The **ID** names for the controls are used in the code for the custom step, so ensure you entered them correctly; otherwise, you will either need to edit the code or the control ID in the properties on the *Design* tab.

  ![](images/CSProgramTab.png)

3. **Save** and close the custom step.

<br>
<br>

## Open and Test the Custom Step in Stand-Alone Mode
1. Select ![SAS Content](images/SASContentIcon.png) to view the **SAS Content** tab in *SAS Studio*.
1. Navigate to **SAS Content &#10132; Public**.
1. Select **GeoDistance with Rounding.step** and right-click to view its menu.
1. Select **Open** to view the custom step in stand-alone mode.

  ![](images/CSOpenStandAlone.png)

<br>
<br>

### Assignment: Test the Custom Step
Perform various tests using **MAPS.AFRICA** as the input table.  Use ![Input Table](images/SelectInputTable.png) to select the input table.

Select columns **X** and **Y** for *Location 1* and columns **LAT** and **LONG** for *Location 2*.

Select **WORK.TEST** as the output table.  Use ![Output Table](images/SelectOutputTable.png) to select the output table.

**Run** the custom step.

![](images/CSTESTResults.png)

View the resulting **TEST** table in the **WORK** library.  Select ![Libraries](images/LibrariesIcon.png) to view the library connections.

![](images/WorkTestResults.png)

Play around with different options on the **Options** tab of the custom step.

**Close** the *TEST* table and the custom step when done.

<br>
<br>

## Use the Custom Step in a SAS Studio Flow
1. In *SAS Studio*, select **New &#10132; Flow** from the menu to create a flow file.

  ![](images/CreateNewFlow.png)

1. x


<br>

## Exercise Completed

You have completed the exercise for **Create Custom Steps with SAS Studio**.

**THANK YOU FOR ATTENDING THIS SESSION!** <br>
**PLEASE COMPLETE THE EVALUATION!**