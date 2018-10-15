---
title: 2018-10-15xmind update8 启动错误
tags: 
grammar_cjkRuby: true
---
发生了错误。请参阅错误日志以了解更多详细信息。

org.eclipse.ui.WorkbenchException: 前言中不允许有内容。
	at org.eclipse.ui.XMLMemento.createReadRoot(XMLMemento.java:147)
	at org.eclipse.ui.XMLMemento.createReadRoot(XMLMemento.java:66)
	at org.xmind.cathy.internal.EditorStatePersistance.recoverLastSession(EditorStatePersistance.java:192)
	at org.xmind.cathy.internal.EditorStatePersistance.startUp(EditorStatePersistance.java:158)
	at org.xmind.cathy.internal.StartUpProcess$2.run(StartUpProcess.java:93)
	at org.eclipse.core.runtime.SafeRunner.run(SafeRunner.java:42)
	at org.xmind.cathy.internal.StartUpProcess.checkAndRecoverFiles(StartUpProcess.java:85)
	at org.xmind.cathy.internal.StartUpProcess.startUp(StartUpProcess.java:49)
	at org.xmind.cathy.internal.CathyWorkbenchAdvisor.postStartup(CathyWorkbenchAdvisor.java:116)
	at org.eclipse.ui.internal.Workbench$58.run(Workbench.java:2956)
	at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine$4.run(PartRenderingEngine.java:1088)
	at org.eclipse.core.databinding.observable.Realm.runWithDefault(Realm.java:336)
	at org.eclipse.e4.ui.internal.workbench.swt.PartRenderingEngine.run(PartRenderingEngine.java:1022)
	at org.eclipse.e4.ui.internal.workbench.E4Workbench.createAndRunUI(E4Workbench.java:150)
	at org.eclipse.ui.internal.Workbench$5.run(Workbench.java:687)
	at org.eclipse.core.databinding.observable.Realm.runWithDefault(Realm.java:336)
	at org.eclipse.ui.internal.Workbench.createAndRunWorkbench(Workbench.java:604)
	at org.eclipse.ui.PlatformUI.createAndRunWorkbench(PlatformUI.java:148)
	at org.xmind.cathy.internal.CathyApplication.start(CathyApplication.java:145)
	at org.eclipse.equinox.internal.app.EclipseAppHandle.run(EclipseAppHandle.java:196)
	at org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.runApplication(EclipseAppLauncher.java:134)
	at org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.start(EclipseAppLauncher.java:104)
	at org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:388)
	at org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:243)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.eclipse.equinox.launcher.Main.invokeFramework(Main.java:673)
	at org.eclipse.equinox.launcher.Main.basicRun(Main.java:610)
	at org.eclipse.equinox.launcher.Main.run(Main.java:1519)
Caused by: org.xml.sax.SAXParseException; lineNumber: 1; columnNumber: 1; 前言中不允许有内容。
	at com.sun.org.apache.xerces.internal.util.ErrorHandlerWrapper.createSAXParseException(ErrorHandlerWrapper.java:203)
	at com.sun.org.apache.xerces.internal.util.ErrorHandlerWrapper.fatalError(ErrorHandlerWrapper.java:177)
	at com.sun.org.apache.xerces.internal.impl.XMLErrorReporter.reportError(XMLErrorReporter.java:400)
	at com.sun.org.apache.xerces.internal.impl.XMLErrorReporter.reportError(XMLErrorReporter.java:327)
	at com.sun.org.apache.xerces.internal.impl.XMLScanner.reportFatalError(XMLScanner.java:1472)
	at com.sun.org.apache.xerces.internal.impl.XMLDocumentScannerImpl$PrologDriver.next(XMLDocumentScannerImpl.java:994)
	at com.sun.org.apache.xerces.internal.impl.XMLDocumentScannerImpl.next(XMLDocumentScannerImpl.java:602)
	at com.sun.org.apache.xerces.internal.impl.XMLDocumentFragmentScannerImpl.scanDocument(XMLDocumentFragmentScannerImpl.java:505)
	at com.sun.org.apache.xerces.internal.parsers.XML11Configuration.parse(XML11Configuration.java:841)
	at com.sun.org.apache.xerces.internal.parsers.XML11Configuration.parse(XML11Configuration.java:770)
	at com.sun.org.apache.xerces.internal.parsers.XMLParser.parse(XMLParser.java:141)
	at com.sun.org.apache.xerces.internal.parsers.DOMParser.parse(DOMParser.java:243)
	at com.sun.org.apache.xerces.internal.jaxp.DocumentBuilderImpl.parse(DocumentBuilderImpl.java:339)
	at org.eclipse.ui.XMLMemento.createReadRoot(XMLMemento.java:120)
	... 30 more

Severity: error
Plug-in ID: org.eclipse.jface
Code: 0

== Environment ==
Time: 2018-10-15 08:49:46
XMind Distribution Pack: cathy_win32
XMind Build ID: R3.7.7.201801311814
Operating System: Windows 10 10.0 (x86)
Platform: win32.win32.x86
Language: zh
Country: CN

== Product ==
Product ID: org.xmind.cathy.product
Application ID: org.xmind.cathy.application
Launcher: XMind

Command Line Arguments: -os
 win32
 -ws
 win32
 -arch
 x86
 -showsplash
 -launcher
 D:\Program Files (x86)\XMind\XMind.exe
 -name
 XMind
 --launcher.library
 D:\Program Files (x86)\XMind\\plugins/org.eclipse.equinox.launcher.win32.win32.x86_1.1.400.v20160518-1444\eclipse_1617.dll
 -startup
 D:\Program Files (x86)\XMind\\plugins/org.eclipse.equinox.launcher_1.3.200.v20160318-1642.jar
 --launcher.overrideVmargs
 -configuration
 @user.home/Application Data/XMind/configuration-cathy_win32-R3.7.7.201801311814
 -data
 @user.home/Application Data/XMind/workspace-cathy
 -eclipse.keyring
 @user.home/Application Data/XMind/secure_storage
 -vm
 D:\Program Files (x86)\XMind\jre\bin\client\jvm.dll
 
VM Arguments: -Dfile.encoding=UTF-8
 -Xms128m
 -Xmx1024m
 -XX:MaxPermSize=256m
 -javaagent:plugins/XMindCrack.jar
 -Djava.class.path=D:\Program Files (x86)\XMind\\plugins/org.eclipse.equinox.launcher_1.3.200.v20160318-1642.jar
 

== Java Properties ==
Java Version: 1.8.0_152
Java Vendor: Oracle Corporation
Java Runtime: Java(TM) SE Runtime Environment
    Version: 1.8.0_152-b16
Java VM: Java HotSpot(TM) Client VM
    Version: 25.152-b16
    Vendor: Oracle Corporation
    Info: mixed mode

