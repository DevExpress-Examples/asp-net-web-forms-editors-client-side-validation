<!-- default badges list -->
![](https://img.shields.io/endpoint?url=https://codecentral.devexpress.com/api/v1/VersionRange/128542134/13.1.4%2B)
[![](https://img.shields.io/badge/Open_in_DevExpress_Support_Center-FF7200?style=flat-square&logo=DevExpress&logoColor=white)](https://supportcenter.devexpress.com/ticket/details/E124)
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
<!-- default badges end -->
# Editors fot ASP.NET Web Forms - How to raise validation on the client
<!-- run online -->
**[[Run Online]](https://codecentral.devexpress.com/e124/)**
<!-- run online end -->

This example demonstrates how to raise client-side validation automatically or on a specific action for a single editor or a group of editors.

## Overview

To automatically raise validation when an editor's value changes to empty, specify the editor's [ValidationSettings](https://docs.devexpress.com/AspNet/DevExpress.Web.ASPxEdit.ValidationSettings) property and set the [RequiredField.IsRequired](https://docs.devexpress.com/AspNet/DevExpress.Web.RequiredFieldValidationPattern.IsRequired) property to `true`. Note that this behavior is enabled when the [ValidateOnLeave](https://docs.devexpress.com/AspNet/DevExpress.Web.ValidationSettings.ValidateOnLeave) property is set to `true`.

```aspx
<dx:ASPxTextBox ID="tbTextBox1" runat="server" Width="170px" Text="Some value">
    <ValidationSettings>
        <RequiredField IsRequired="True" ErrorText="Field is required." />
    </ValidationSettings>
</dx:ASPxTextBox>
```

To validate edit values on a specific action (for example, on a button click), call the client-side [Validate](https://docs.devexpress.com/AspNet/js-ASPxClientEdit.Validate) method. To disable automatical validation when the editor's value changes, set the [ValidateOnLeave](https://docs.devexpress.com/AspNet/DevExpress.Web.ValidationSettings.ValidateOnLeave) property to `false`.

```aspx
<input type="button" value="Validate" onclick="ASPxClientControl.GetControlCollection().GetByName('tbTextBox2').Validate();" style="width: 127px;" />
<dx:ASPxTextBox ID="tbTextBox2" runat="server" ClientInstanceName="tbTextBox2" Width="170px">
    <ValidationSettings ValidateOnLeave="False">
        <RequiredField IsRequired="True" ErrorText="Field is required." />
    </ValidationSettings>
</dx:ASPxTextBox>
```

To validate values in a group of editors on a specific action, disable editors' [ValidateOnLeave](https://docs.devexpress.com/AspNet/DevExpress.Web.ValidationSettings.ValidateOnLeave) properties, set [ValidationGroup](https://docs.devexpress.com/AspNet/DevExpress.Web.ValidationSettings.ValidationGroup) properties to a common value, and pass this value to the client-side [ValidateGroup](https://docs.devexpress.com/AspNet/js-ASPxClientEdit.ValidateGroup.static(validationGroup)) method.

```aspx
<dx:ASPxTextBox ID="tbTextBox3" runat="server" Width="170px" Style="margin-bottom: 4px;">
    <ValidationSettings ValidationGroup="MyGroup" ErrorText="Field is required." ValidateOnLeave="False">
        <RequiredField IsRequired="True" ErrorText="" />
    </ValidationSettings>
</dx:ASPxTextBox>
<dx:ASPxTextBox ID="tbTextBox4" runat="server" Width="170px">
    <ValidationSettings ValidationGroup="MyGroup" ErrorText="Field is required." ValidateOnLeave="False">
        <RequiredField IsRequired="True" ErrorText="" />
    </ValidationSettings>
</dx:ASPxTextBox>
<br />
<input type="button" value="Validate Group" onclick="ASPxClientEdit.ValidateGroup('MyGroup');" />
```

To validate values in a group of editors on a postback, enable editors' [AutoPostBack](https://docs.devexpress.com/AspNet/DevExpress.Web.ASPxEdit.AutoPostBack), [ValidateOnLeave](https://docs.devexpress.com/AspNet/DevExpress.Web.ValidationSettings.ValidateOnLeave), and [CausesValidation](https://docs.devexpress.com/AspNet/DevExpress.Web.ValidationSettings.CausesValidation) properties and set their [ValidationGroup](https://docs.devexpress.com/AspNet/DevExpress.Web.ValidationSettings.ValidationGroup) properties to a common value. When an editor's value changes, validation is raised for all editors in the specified group.

```aspx
<dx:ASPxComboBox ID="cbComboBox2" runat="server" AutoPostBack="True">
    <Items>
        <!-- ... -->
    </Items>
    <ValidationSettings CausesValidation="True" ValidationGroup="CausesValidationDemoGroup">
        <RequiredField IsRequired="True" ErrorText="Select not empty value." />
    </ValidationSettings>
</dx:ASPxComboBox>
<br />
<dx:ASPxComboBox ID="cbComboBox3" runat="server" AutoPostBack="True">
    <Items>
        <!-- ... -->
    </Items>
    <ValidationSettings CausesValidation="True" ValidationGroup="CausesValidationDemoGroup">
        <RequiredField IsRequired="True" ErrorText="Select not empty value." />
    </ValidationSettings>
</dx:ASPxComboBox>
```

## Files to Review

* [Default.aspx](./CS/WebSite/Default.aspx) (VB: [Default.aspx](./VB/WebSite/Default.aspx))
