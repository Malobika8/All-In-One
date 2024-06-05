# CustomPropertyEditor

<img width="1014" alt="Screenshot 2024-06-04 at 11 07 39 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/51271113-e6b5-4c9c-a4af-b31f50b70b19">
<img width="937" alt="Screenshot 2024-06-04 at 11 08 19 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/9e518f92-232e-4512-8567-b7cb83fb97ba">

To create our own PropertyEditor, we need to extend PropertyEditorSupport.

Consider a scenario where if we provide our name during registration, our name should be shown in all caps in the registration successful page. In such case, we need to convert our name(add a new property editor) in init binder before passing details to registration successful page.

Create a new PropertyEditor class. It should extend PropertyEditorSupport. Override "setAsText()" method and then resgister the new Property Editor with WebDataBinder in initBinder method.
*Note:* All the Editor classes should always extend PropertyEditorSupport.

<img width="1264" alt="Screenshot 2024-06-05 at 8 30 53 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/947ce0dc-2441-445a-8626-30c72f1d394e">
<img width="1044" alt="Screenshot 2024-06-05 at 8 31 07 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/b0c81c38-4cbb-472d-9abe-a14e960d7210">

Run the application

<img width="893" alt="Screenshot 2024-06-05 at 8 32 18 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/98cd5408-14bd-41eb-9b62-58041e0f61b7">

Note that the name now shows in all caps in Registration Successful page.

<img width="716" alt="Screenshot 2024-06-05 at 8 32 36 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/139f6343-1e90-4554-9664-084ad0ad45d1">

### Another use of InitBinder:

It can also be used to register Formatters. instead of registering in the config class, we can also make use of WebDataBinder to addthe Custom Formatter.

<img width="965" alt="Screenshot 2024-06-05 at 9 14 48 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/90678dee-e8a6-4cc3-9d2f-22f7b2a137df">
<img width="986" alt="Screenshot 2024-06-05 at 9 13 06 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/21b25a39-5fd2-4af7-82de-accc918ad33b">
<img width="1015" alt="Screenshot 2024-06-05 at 9 16 16 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/1e703b5e-1763-4e56-801a-fe19f8bab796">

## Formatter VS Editor

These two have very similar concept and can be used interchangaebly in most cases.
Similar to how we use "print" method in Formatter, we can use "getAsText" method in Editor.

### Which one to use though? Formatter or Editor?

Should we use a Formatter(and use print and parse method) or PropertEditor(and use setAsText and getAsText method)?
