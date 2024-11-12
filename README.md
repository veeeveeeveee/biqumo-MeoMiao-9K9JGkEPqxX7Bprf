
使用Flask编写一个网站是一个相对简单且有趣的过程。Flask是一个用Python编写的轻量级Web应用框架。它易于上手，同时也非常强大，适合构建从简单的博客到复杂的Web应用的各种项目。以下是一个使用Flask编写简单网站的指南，包括代码示例。


## 一、如何使用Flask编写一个网站


### （一）安装Flask


首先，我们需要确保我们的Python环境中安装了Flask。我们可以使用pip（Python的包管理器）来安装它。



```
bash复制代码

pip install Flask

```

### （二）创建Flask应用


1. **创建项目目录**：
在我们的计算机上创建一个新的目录来存放我们的Flask项目。
2. **创建主应用文件**：
在项目目录中创建一个名为`app.py`（或我们喜欢的任何名称）的文件，并添加以下代码：



```
# app.py
from flask import Flask, render_template, request
 
app = Flask(__name__)
 
# 配置项（可选）
app.config['DEBUG'] = True  # 开启调试模式，这样代码变动后服务器会自动重启
 
# 路由和视图函数
@app.route('/')
def home():
    return render_template('index.html')  # 渲染模板文件
 
@app.route('/greet', methods=['GET', 'POST'])
def greet():
    if request.method == 'POST':
        name = request.form['name']  # 从表单中获取数据
        return f'Hello, {name}!'
    return render_template('greet.html')  # 渲染表单模板
 
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)  # 在所有网络接口上运行，监听5000端口

```

### （三）创建HTML模板


1. **创建模板目录**：
在项目目录中创建一个名为`templates`的文件夹。
2. **添加模板文件**：
在`templates`文件夹中创建两个HTML文件：`index.html`和`greet.html`。


`index.html`：



```
html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hometitle>
head>
<body>
    <h1>Welcome to My Flask Websiteh1>
    <a href="/greet">Greet Someonea>
body>
html>

```

`greet.html`：



```
html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Greettitle>
head>
<body>
    <h1>Greet Someoneh1>
    <form method="post">
        <label for="name">Name:label>
        <input type="text" id="name" name="name">
        <button type="submit">Submitbutton>
    form>
body>
html>

```

### （四）运行Flask应用


1. **打开终端**：
打开我们的命令行界面（终端、命令提示符等）。
2. **导航到项目目录**：
使用`cd`命令导航到我们创建的项目目录。
3. **运行应用**：
在终端中运行以下命令来启动Flask应用：



```
bash复制代码

python app.py

```

1. **访问网站**：
打开我们的网络浏览器，并访问`http://localhost:5000/`。我们会看到“Welcome to My Flask Website”的页面。点击“Greet Someone”链接，我们会被带到表单页面。填写表单并提交，我们会看到问候信息。


### （五）调试和部署


* **调试**：如果我们开启了调试模式（`app.config['DEBUG'] = True`），当我们修改代码并保存时，Flask应用会自动重启，以便我们立即看到更改的效果。
* **部署**：将Flask应用部署到生产环境通常涉及使用WSGI服务器（如Gunicorn或uWSGI）和反向代理（如Nginx或Apache）。这超出了这个简单指南的范围，但我们可以查阅Flask的官方文档或搜索相关的教程来了解更多信息。


通过以上步骤，我们已经成功地使用Flask编写了一个简单的网站。现在，我们可以继续扩展我们的网站，添加更多的路由、模板和逻辑来满足我们的需求。


## 二、如何在Flask中添加样式表


在Flask中添加样式表（CSS）是一个常见的需求，它允许我们自定义网页的外观和感觉。以下是如何在Flask项目中添加和使用样式表的步骤：


### （一）创建静态文件夹


Flask有一个约定，即所有静态文件（如CSS、JavaScript、图片等）都放在名为`static`的文件夹中。如果我们的项目目录中还没有这个文件夹，请创建一个。


### （二）添加样式表文件


在`static`文件夹中，创建一个新的CSS文件，比如`styles.css`。


### （三）编写CSS代码


在`styles.css`文件中编写我们的CSS代码。例如：



```
/* styles.css */
body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    margin: 0;
    padding: 0;
}
 
h1 {
    color: #333;
}
 
.container {
    width: 80%;
    margin: 0 auto;
    padding: 20px;
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

```

### （四）在HTML模板中链接样式表


现在，我们需要在HTML模板中链接这个CSS文件。使用标签，并将`href`属性设置为样式表的相对路径（从`static`文件夹开始）。


例如，在我们的`index.html`模板中：



```
html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Flask Websitetitle>
    <link rel="stylesheet" href="{{ url_for('static', filename='styles.css') }}">
head>
<body>
    <div class="container">
        <h1>Welcome to My Flask Websiteh1>
        <p>This is a simple Flask web application with a custom stylesheet.p>
    div>
body>
html>

```

注意这里使用了`{{ url_for('static', filename='styles.css') }}`来生成样式表的URL。这是Flask提供的一个帮助函数，它可以确保我们的静态文件路径是正确的，即使我们将应用部署到不同的URL或子路径上。


### （五）运行Flask应用


确保我们的Flask应用正在运行，然后访问我们的网页。我们能看到应用了CSS样式的网页。


### （六）调试和修改


如果样式没有正确应用，检查以下几点：


* 确保`static`文件夹和`styles.css`文件的路径正确。
* 确保在HTML模板中正确使用了标签。
* 清除浏览器缓存，以确保我们看到的是最新的CSS文件。
* 使用浏览器的开发者工具（通常可以通过按F12或右键点击页面并选择“检查”来打开）来检查是否有任何错误或警告。


通过以上步骤，我们能够成功地在Flask项目中添加和使用样式表。


## 三、如何在Flask中添加图片


在Flask中添加图片与添加样式表类似，我们需要将图片文件放在指定的静态文件夹中，并在HTML模板中引用它们。以下是详细步骤：


### （一）创建或确认静态文件夹


确保我们的Flask项目中有一个名为`static`的文件夹。这个文件夹用于存放所有的静态文件，包括图片、CSS文件、JavaScript文件等。


### （二）添加图片文件


将我们的图片文件（如`example.png`）放入`static`文件夹中。我们可以在这个文件夹内创建一个子文件夹来组织我们的图片，比如`static/images/`。


### （三）在HTML模板中引用图片


在我们的HTML模板中，使用`![]()`标签来引用图片。由于图片存放在`static`文件夹中，我们需要使用相对路径来引用它们。Flask提供了一个帮助函数`url_for`来生成静态文件的URL，但对于图片来说，直接使用相对路径通常更简单且直观。


例如，如果我们的图片存放在`static/images/`文件夹中，我们可以在HTML模板中这样引用它：



```
html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Flask Website with Imagestitle>
head>
<body>
    <h1>Welcome to My Flask Websiteh1>
    <p>Here is an example image:p>
    <img src="{{ url_for('static', filename='images/example.png') }}" alt="Example Image">
    
    
body>
html>

```

注意，这里展示了两种引用图片的方法：


1. 使用`url_for`函数，这是Flask推荐的方式，因为它可以处理路径和URL的更改。
2. 使用相对路径，这种方法更简单，但在某些情况下（如应用部署在子路径上时）可能会遇到问题。


### （四）运行Flask应用


确保我们的Flask应用正在运行，然后访问我们的网页。我们能看到引用的图片显示在网页上。


### （五）调试和修改


如果图片没有正确显示，检查以下几点：


* 确保`static`文件夹和图片文件的路径正确。
* 确保在HTML模板中正确使用了`![]()`标签和`src`属性。
* 清除浏览器缓存，以确保我们看到的是最新的图片文件。
* 检查图片文件的权限，确保Web服务器可以访问它们。
* 使用浏览器的开发者工具来检查是否有任何错误或警告，特别是关于图片加载失败的错误。


通过以上步骤，我们能够成功地在Flask项目中添加和显示图片。


 本博客参考[楚门加速器](https://chuanggeye.com)。转载请注明出处！
