# 1.
```python
# -*- coding: utf-8 -*-
```
# 2.
```python
class TextBrowserSample(QMainWindow):
    def __init__(self):
        super(TextBrowserSample, self).__init__()
        uic.loadUi('TextBrowserSample.ui', self)
        self.loadButton.clicked.connect(self.load_file)
        self.processButton.clicked.connect(self.process_data)

    def load_file(self):
        try:
            with open('input.txt', 'r',
                      encoding='utf8') as f:  
                # Если файла нет, то мы получим исключение FileNotFoundError
                self.inputText.setText(f.read())
        except FileNotFoundError as ex:
            self.statusBar().showMessage('В директории нет файла input.txt')

    def process_data(self):
        data = self.inputText.toPlainText()
        self.outputText.setText(data[::-1])

    def color_text(self):
        data = self.inputText.toPlainText()
        HTML = ""
        for i in data:
            color = "#{:06x}".format(random.randrange(0, 0xFFFFFF))
            HTML += "<font color='{}' size = {} >{}</font>".format(
                color, random.randrange(1, 8), i)
        self.outputText.setHtml(HTML)
```