+++
title = "Multi language locale based menu for Arduino and mbed"
description = ""
tags = "arduino, multi-language, embedded-menu, library"
type = "blog"
date = "2023-05-30"
author =  "dave"
menu = "tc-menu"
banner = "/products/arduino-libraries/images/electronics/arduino/tcMenu/oled-dashboard-example.jpg"
titleimg = "/products/arduino-libraries/images/electronics/arduino/tcMenu/oled-dashboard-example.jpg"
githublink = "https://github.com/TcMenu/tcMenu"
referenceDocs = "/tcmenu/html/index.html"
weight = 2
toc_needed = true
+++

tcMenu supports compile-time internationalisation using Java-style [resource bundles](https://www.baeldung.com/java-resourcebundle). You define translated strings in an `i18n` directory, refer to those strings from your menu definition or C++ code, and the code generator creates C++ headers for the selected language.

We enable the support by adding an `i18n` directory within the project that has at least a properties file named `project-lang.properties` within it. You can either enable it within [TcMenu Web Designer](https://designer.thecoderscorner.com), or manually set up the directories yourself.

Once you've enabled i18n support, each menu item (and even additional strings in your application) can be localized. The method is slightly different for manually maintained menu builder fluent API and static projects. Each is described in detail later.

## Summary of locale project storage 

Let's take a project that has been localized to both English and French. We normally always treat English as the default language. Notice the i18n directory at the same level as the `emf` project file with properties files within it.

    projectDirectory
        projectName.emf
        i18n
            project-lang.properties
            project-lang_fr.properties

Here is an example properties file:

    menu.3.enum.1=Item2
    menu.3.enum.0=Item 1
    menu.3.name=Enum
    project.name=Adafruit Dashboard

We can see that entries are in the form `key=value`. If you're using fluent API instead of round tripping, whereever you could provide a `const char*` AKA a constant string of characters such as `"hello world"` you can replace with a localized string.

There are many good editors that support resource bundles, including most Jetbrains IDEs and VS Code.

Code generator itself supports locale entries for:

* `name` field of any item, 
* `AnalogMenuItem` `unit` field, 
* `EnumMenuItem` `entries`, 
* `ListMenuItem` menu item values, 
* and the project name field.

## How properties are mapped to C++ header definitions

Every build of the locale header files (either using designer or the simple Python script build tool) converts properties files into C++ header definitions. There is a section for every language, and you can choose between them using `TC_LOCALE_??` build flag. In the header file, each property name is converted into a header define by prefixing with `TC_I18N_`, turning all letters to upper case, replacing all dots with underscores. For example:

      # in the properties file
      my.property.name=hello world

      // C++ code header - can be used in code needing a const char[] / string.
      #define TC_I18N_MY_PROPERTY_NAME="hello world"

We plan to soon add support for changing languages at runtime, but this requires a little work. However, when you're using the locale definitions above, access the values using this function as that will eventually allow for runtime language switching. Here are two code examples:

     const char* myStr = getTcLocaleString(TC_I18N_MY_PROPERTY_NAME);
     auto len = strllen(getTcLocaleString(TC_I18N_MY_PROPERTY_NAME));

Although at the moment this is passthrough, it will eventually work with a global locale object.

## How to localize a menu project

There are two different ways that you can use [tcMenu Web Designer](https://designer.thecoderscorner.com), you can either create an initial project in web designer using the fluent menu builder pattern, and then maintain it yourself. Using this pattern you do not round trip and modify the structure yourself. The second way is to let tcMenu Designer look after the menu structures for you and round trip changes through designer.

Either method works for internationalized menus, and each is discussed in detail below.

### Localizing TcMenuBuilder project that is manually maintained 

For this case, use the python `tcmenu-i18n` script from the tcMenu repository, this builds the properties into header files after you've changed them. It has the following options:

* `--single-hdr` generate all locales into a single header file (without this option you get one header per language).
* `--out-dir` generate files into a directory relative to the starting point.

The procedure is:

* Edit the `i18n/tcmenu-lang*.properties` properties files to add your new translations.
* Run the `tcmenu-i18n` script to generate the header files.
* Include the generated header files in your project files.
* Use the translation strings using `getTcLocaleString(...)` as described above.

For example using the a property in a float builder item:

```
    TcMenuBuilder builder(...);
    builder.floatItem(MENU_ITEM_ID, getTcLocaleString(TC_I18N_ITEM_NAME), DONT_SAVE, 1, NoMenuFlags)
```

### Localizing a menu built by designer round-trip generation

To localize a string, simply prepend the name/unit/value in either designer or the `emf` file so that it starts with a `%`; which means localize the value with translations in the resource bundle. The exception is `%%` which escapes the `%` symbol. Resource bundles are fully documented in many places online, this is just a getting started guide. 

For example if we set the unit of an analog item in designer to `%menu.1.unit` we would then need to add a line to the properties as follows:

       menu.1.unit=Amp

To escape a `%` at the start of the text we use the following `%%` that means `%`.

In web designer, it will try to load the default properties file, and show the values from there in the menu tree.

Take careful note that although there are extended save locations, where you can generate files into a `generated` directory that this is incompatible with Arduino UI or CLI, only use this with CMake and PlatformIO.

<figure><img src="/products/arduino-libraries/images/electronics/arduino/tcMenu/generatorui-locale-save-locations.png" alt="Possible save locations for both your and the generated code" /><figcaption>Choosing a save location</figcaption></figure>

### When you're using all plugins in single file mode

In the case that all plugins in single file mode is selected, then all the locales will be written into a single file. They will all be written into `projectName_langSelect.h`.

### When you're using separate plugin per file mode

In the generated output directory there will be several new files. Firstly `projectName_langSelect.h` that will include the right language header file based on a compile time flag, then each of the language files following the pattern `projectName_lang.h`. Here's an example:

## How values are interpolated

When generating the properties file, the precidence will be firstly the most language specific file, working out to the default file. For example, if you're targeting English and French, you'd have the main file contianinig English, and  `project-lang_fr.properties` for the French translations. Any missing entries in the French (or other chosen language) properties default to the English text. You can also use country level locales too, these are supported by both the round trip and the python script.

Order of precedence:

* Country specific file (E.G. French/Candadian)
* Language specific file (E.G. French)
* Default file

Example French property file content:

    menu.1.name = Bonjour

Example property file content:

    menu.1.name = Hello
    menu.1.unit = V

| Field        | Output  | Language          | Comment                                           |
|--------------|---------|-------------------|---------------------------------------------------|
| %menu.1.name | Hello   | English (default) | Taken from default bundle                         |
| %menu.1.name | Bonjour | French (fr)       | Taken from French bundle                          |
| %menu.1.unit | V       | French (fr)       | Taken from default bundle as not in French bundle |
| %%           | %       | Any               | Escaped to %                                      |
| Text         | Text    | Any               | Not from bundle                                   |
| V            | V       | Any               | Not from bundle                                   |

## Editing items in designer (round trip mode)

In web designer, once an application is internationalized, you'll see that the items in the tree will show the default translation text, when you use a resource bundle reference. For example, if you type in `%menu.1.name` it will show "Hello" in the preview. If you type in `Text` it will show "Text" in the preview. If you type in `%%` it will show "%" in the preview.

Also, the root menu contains a refresh properties button that allows you to reload the properties from the resource bundle.

    generated
        projectName_lang.h
        projectName_lang_fr.h
        projectName_langSelect.h
        projectName_menu.cpp
        projectName_menu.h

## Choosing a locale

Always only include `projectName_langSelect.h` as this will select the right locale. Locales use the standard language and country format. For example to choose global French set the follow compile flag:

    TC_LOCALE_FR

The lack of such a compile flag means use the default locale. Even most TcMenu internal strings are now localized and use the same locale definition file, there are presently translations into English, French, Slovak, German, Ukrainian, and Czech. Any other translations would be greatly welcomed, see the tcMenuLib github repo.
