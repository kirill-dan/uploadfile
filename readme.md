По просьбам трудящихся создал простенький плагин к WEB редактору Summernote 0.8.8

Плагин позволяет в диалоговом окне выбрать файл с диска, написать заголовок, и отметить чекбокс, 
нужно ли будет файл открывать по ссылке в новом окне.

Файл будет сохранен на диск через функцию ajax, будет создана ссылка на файл и вставлена в редактор.

В плагине реализована только фронтовая часть. Бэкенд нужно делать самому.

Пару моментов:

1. В функции замыкания Uploadfile содержится переменная editor. По умолчанию сейчас стоит: 
```
var editor = $('#summernote');
```

Вам нужно будет установить свой идентификатор или класс редактора, если вы используете другие значения.

2. Кидаете плагин в папку плагинов summernote

3. Подключаете плагин после инициализации файла с настройками редактора, например так (в примере для Ларавел):
```
{{-- Include uploadfile plugin --}}
<script src="{!! asset('editors/summernote/plugin/uploadfile/summernote-ext-uploadfile.js') !!}"></script> 
```

4. В файле настроек к тулбару подключаете сам плагин:
```
toolbar: [
  ['uploadfile', ['uploadfile']],
],
```

5. Аякс будет отдавать файл постом на ссылку: /ajax/uploader/save-file 
Переменная: files
Все проверки того, что вам пытаются загрузить лежат на вас. Так же, как и сам процесс сохранения файла.
После сохранения файла возвращаете на него ссылку. Просто текстом. Например (для PHP): 
```
return 'https://mydomen.com/myfile.ext';
```

Времени тщательно тестировать плагин нет, так что сами проверяйте и отписывайтесь. У меня заработал.

Обсуждение можно вести здесь: https://cleverman.org/post/38
