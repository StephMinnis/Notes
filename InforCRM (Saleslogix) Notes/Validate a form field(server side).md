
### Adding a Form Data Validation

About:  This document walks you through how to set up a server side data validation for a form field



#### In Application Architect LFS→Entity Model→Packages→Saleslogix Application Entities:

*Open the form you would like to add a validation to ex:  Opportunity→OpportunityDetails

*Switch from design to code view in the tabs at the bottom of the Quickform Details window

*Right click your field's Control action ex: QFTextBox→OnChangeAction

*Click Add → C# Snippet Action Item

.*This example uses Regex to verify that there are only numbers and that the data entered is only a 4 digit entry

``` 
Regex r = new Regex("^[0-9]{1,4}$");		
if (!String.IsNullOrEmpty(QFTextBox.Text)){
if (!r.IsMatch(QFTextBox.Text))
			   throw new Sage.Platform.Application.ValidationException("Month to Ship must be a four digit number (like 1801 for 2018-JAN) ");
}
```

*Save, build and deploy