---
layout: post
title: "CustomAttributeFormatException in VS2010 Beta 1"
date: 2009-06-01 23:57
comments: true
categories: 
alias: [/archive/2009/06/01/customattributeformatexception-in-vs2010-beta-1.aspx]
---
I’ve been doing some development recently with Visual Studio 2010 Beta 1 and because of this I ran across a bug in .NET 4.0 Beta 1:

{% img /images/archive/CustomAttributeFormatException.png CustomAttributeFormatException %}

This cropped up when I decided to introduce logging into my application using the [Microsoft Enterprise Library](http://entlib.codeplex.com/). I soon found out that the current version of the Enterprise Library will not work with .NET 4.0 Beta 1 due to [an existing bug](http://entlib.codeplex.com/Thread/View.aspx?ThreadId=56814).

The quick fix to this is to make sure your project is targeting .NET 3.5 SP1, which my project already was. After some more digging around I realized that though I was targeting 3.5, Visual Studio was hosting my WCF service using its .NET 4.0 version of WcfSvcHost.exe.

The workaround that I’ve created involves pointing my project to the VS 2008 version of the WCF Service Host for debugging purposes:

{% img /images/archive/Project_Properties.png Project Properties %}

The external program path I’m using is “C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\WcfSvcHost.exe”, though your path may vary. I set the working directory to my project’s debug directory.

[Here](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=444020) is the direct link to the Microsoft Connect bug report in case you want to validate it or vote it up.