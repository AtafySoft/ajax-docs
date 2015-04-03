---
title: Track Changes
page_title: Track Changes | UI for ASP.NET AJAX Documentation
description: Track Changes
slug: editor/functionality/track-changes-and-comments/track-changes
tags: track,changes
published: True
position: 0
---

# Track Changes



This article shows how to enable, configure and use the built-in __Track Changes__ feature of the __Telerik Editor for ASP.NET AJAX__.

The __Track Changes__ feature is available since __Q2 2012__.
>caption Figure 1: RadEditor with Tracked Changes enabled.

![editor-track-changes-enabled](images/editor-track-changes/editor-track-changes-enabled.png)

Quick navigation:

1. [Overview](#overview)

1. [Enabling Track Changes Feature and Tools](#enabling-track-changes-feature-and-tools)

1. [User Configuration](#user-configuration)

1. [Generated HTML](#generated-html)

1. [Client-side Methods](#client-side-methods)

1. [Server-side Methods](#server-side-methods)

1. [Supported Commands](#supported-commands)

## Overview

The __Track Changes__ feature enables end-users to keep track of the changes made when editing the content in the__RadEditor__. Changes are tracked when e.g., applying text formatting to a text selection, entering new content,deleting existing one, etc (__Figure 1__). Additionally, on selecting a tracked change a little popup with details aboutit will appear at the bottom right corner of the browser or the relative positioned parent (__Figure 2__).
>caption Figure 2: Popup dialog with details about the selected tracked change.

![editor-track-changes-details-popup](images/editor-track-changes/editor-track-changes-details-popup.png)

Further, the tracked change(s) can be accepted or rejected based on the set user permissions(you can check how to configure the user settings in the [User Configuration](#user-configuration) section).

The __Track Changes__ feature comes with built-in tools that enables the user to enable/disable the feature,and to accept or reject track changes in the content. The following list provides descriptions for all of the provided tools:

* __Accept Track Change__ - click the button to accept the last change

* __Reject Track Change__ - press the button to reject the selected change

* __Accept All Track Changes__ - accepts all changes in the document

* __Reject All Track Changes__ - rejects all changes in the document

* __Enable Track Changes Override__ - turns Track Changes on or off

## Enabling Track Changes Feature and Tools

The following steps will guide you on enabling the __Track Changes__ feature and adding the tools in the__RadEditor__ toolbar:

1. Set the __EnableTrackChanges__ property to __true__:

````ASPNET
			<telerik:RadEditor runat="server" ID="RadEditor1" EnableTrackChanges="true">
			</telerik:RadEditor>
	
````



1. Enable the built-in __Track Changes__ tools:

>tabbedCode

````ASPNET
			<telerik:RadEditor runat="server" ID="RadEditor1" EnableTrackChanges="true">
				<Tools>
					<telerik:EditorToolGroup>
						<telerik:EditorTool Name="AcceptTrackChange" />
						<telerik:EditorTool Name="RejectTrackChange" />
						<telerik:EditorTool Name="AcceptAllTrackChanges" />
						<telerik:EditorTool Name="RejectAllTrackChanges" />
						<telerik:EditorTool Name="EnableTrackChangesOverride" />
					</telerik:EditorToolGroup>
				</Tools>
			</telerik:RadEditor>
````



````C#
			RadEditor1.EnsureToolsFileLoaded(); // Load default set of tools
			EditorToolGroup trackChangesTools = new EditorToolGroup();
	
			trackChangesTools.Tools.Add(new EditorTool("AcceptTrackChange"));
			trackChangesTools.Tools.Add(new EditorTool("RejectTrackChange"));
			trackChangesTools.Tools.Add(new EditorTool("AcceptAllTrackChanges"));
			trackChangesTools.Tools.Add(new EditorTool("RejectAllTrackChanges"));
			trackChangesTools.Tools.Add(new EditorTool("EnableTrackChangesOverride"));
	
			RadEditor1.Tools.Add(trackChangesTools);
````



````VB.NET
			RadEditor1.EnsureToolsFileLoaded() ' Load default set of tools
			Dim trackChangesTools As EditorToolGroup = New EditorToolGroup
	
			trackChangesTools.Tools.Add(New EditorTool("AcceptTrackChange"))
			trackChangesTools.Tools.Add(New EditorTool("RejectTrackChange"))
			trackChangesTools.Tools.Add(New EditorTool("AcceptAllTrackChanges"))
			trackChangesTools.Tools.Add(New EditorTool("RejectAllTrackChanges"))
			trackChangesTools.Tools.Add(New EditorTool("EnableTrackChangesOverride"))
	
			RadEditor1.Tools.Add(trackChangesTools)
````



````XML
			<tools name="TrackChangesToolbar">
			  <tool name="AcceptTrackChange" Text="Accept Track Change"/>
			  <tool name="RejectTrackChange" Text="Reject Track Change"/>
			  <tool name="AcceptAllTrackChanges" Text="Accept All Track Changes"/>
			  <tool name="RejectAllTrackChanges" Text="Reject All Track Changes"/>
			  <tool name="EnableTrackChangesOverride" Text="Enable Track Changes Override"/>
			</tools>
````


>end

At this point, the __Track Changes__ feature is ready to be used by end-users.Changes can be tracked in the text and the built-in tools are provided in the toolbar.

By default, the tracked changes cannot be accepted or rejected, because the initial usersetting restricts it, i.e., the corresponding tools are disabled. Optionally, you canalter the user settings by reconfiguring the __TrackChangesSettings__ where you can change the__Author__, __UserCssId__ and __CanAcceptTrackChanges__ properties.The following section will explain more details about these properties.

## User Configuration

In __Track Changes__ the user settings are the way to define the name of the editor,what stylization are applied based on the settings and configure if changes can be accepted/rejected.

These setting are available in the __TrackChangesSettings__ inner tag, where the following properties are exposed:

* __Author__—the name with which the editor to be recognized.

* __UserCssId__—the class name that defines the color of the changes made in the content. There are ten ready-to-use, predefined classes	(reU0, reU1, reU2, reU3, reU4, reU5, reU6, reU7, reU8, reU9).

* __CanAcceptTrackChanges__—a Boolean property that defines if the user can accept and reject changes.

__Example 1__: Using TrackChangesSettings to define user settings

>tabbedCode

````ASPNET
			<telerik:RadEditor runat="server" ID="RadEditor1" EnableTrackChanges="true">
				<TrackChangesSettings Author="AuthorName" CanAcceptTrackChanges="true" UserCssId="reU0" />
			</telerik:RadEditor>
````



````C#
			RadEditor1.TrackChangesSettings.Author = "AuthorName";
			RadEditor1.TrackChangesSettings.UserCssId = "reU0";
			RadEditor1.TrackChangesSettings.CanAcceptTrackChanges = "true";
````



````VB.NET
			RadEditor1.TrackChangesSettings.Author = "AuthorName"
			RadEditor1.TrackChangesSettings.UserCssId = "reU0"
			RadEditor1.TrackChangesSettings.CanAcceptTrackChanges = "true"
````


>end

Optionally, you can use a custom __UserCssId__ value and define custom appearance for it. To do so you should implement a CSSfile with CSS rules like the ones in __Example 2__. This file should be imported into the RadEditor’s content area via the[CssFiles collection]({%slug editor/functionality/toolbars/dropdowns/external-css-files%}) or the[ContentAreaCssFile property]({%slug editor/managing-content/content-area-appearance/custom-stylization%}) only if the[ContentAreaMode property]({%slug editor/functionality/editor-views-and-modes/contentareamode-property%}) is set to Iframe. If the Div mode is set, theCSS file should be directly imported in the main page.

__Example 2__: Custom styles for the reU10 UserCssId value

````XML
	        /*User border and text colors*/
	        ins.reU10, del.reU10
	        {
	            color: #00FFCC !important;
	        }
	        
	        /* user border colors */
	        .reFormat.reU10,
	        ins.reU10 table,
	        del.reU10 table,
	        ins.reU10 td,
	        ins.reU10 img,
	        del.reU10 td,
	        del.reU10 img,
	        .reComment.reU10
	        {
	            border-color: #00FFCC;
	        }
````



## Generated HTML

The __Track Changes__ functionality entirely relies on HTML to show, recognize and manipulate the tracked content.Upon user interaction __Track Changes__ adds and/or modifies the HTML output with additional tags and attributes whichrepresent the actual tracked change. The examples listed below show the HTML generation upon some user interactions:

* Text insertion:

````HTML
	    <ins class="reU0" title="Inserted by RadEditorUser on 10/20/2014, 6:29:54 PM" 
			timestamp="1413818994783" command="Insert" author="RadEditorUser">some content</ins>
````



* Text deletion:

````HTML
	    <del class="reU0" title="Deleted by RadEditorUser on 10/20/2014, 6:30:45 PM" 
			timestamp="1413819045036" command="Delete" author="RadEditorUser">some content</del>
````



* Text replacement:

````HTML
	    <del class="reU0" title="Deleted by RadEditorUser on 10/20/2014, 6:31:11 PM" 
			timestamp="1413819071182" command="Delete" author="RadEditorUser">some content</del>
	
		<ins class="reU0" title="Inserted by RadEditorUser on 10/20/2014, 6:31:11 PM" 
			timestamp="1413819071185" command="Insert" author="RadEditorUser">inserted content</ins>
````



* Text replacement:

````HTML
	    <strong class="reFormat reU0" title="Formatted by RadEditorUser on 10/20/2014, 6:32:39 PM" 
			timestamp="1413819159465" command="Bold" author="RadEditorUser">some content</strong>
````



## Client-Side Methods

Enabling the Track Changes feature enables you to use the following client-side methods:

* __get_htmlAcceptChanges()__-returns HTML content as if Accept All Track Changes is fired.

* __get_htmlRejectChanges()__-returns HTML content as if Reject All Track Changes is fired.

## Server-side Methods

Since __Q3 2012____Track Changes__ feature also exposes new server-side methods for accepting and rejecting the changes:

* __AcceptTrackChanges()__-changes the content of RadEditor by accepting the track changes..

* __RejectTrackChanges()__-changes the content of RadEditor by rejecting the track changes.

## Supported Commands

The following commands are officially supported by __Track Changes__ and are designed to work with tracked content:

* Bold

* Italic

* Underline

* Indent

* Outdent

* JustifyLeft

* JustifyRight

* JustifyCenter

* JustifyFull

* Superscript

* Subscript

* Insert Table

* Insert Link

* Insert Ordered List

* Insert Unordered List

The addition of new commands is planned for the upcoming releases. If you want to see a command implemented let us know to raise its priority.

# See Also

 * [External CSS Files]({%slug editor/functionality/toolbars/dropdowns/external-css-files%})

 * [Custom Stylization]({%slug editor/managing-content/content-area-appearance/custom-stylization%})

 * [ContentAreaMode Property]({%slug editor/functionality/editor-views-and-modes/contentareamode-property%})

 * [Comments]({%slug editor/functionality/track-changes-and-comments/comments%})