# Как сделать видео фоном для текста

## Демонстрация

![демонстрация](/pictures/video-background.gif)

## Код

```html
<!doctype html>
<html lang="en">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Encode+Sans+SC&display=swap" rel="stylesheet">
<head>
    <meta charset="UTF-8">
    <title>Видео в качестве заднего фона</title>
    <style>
        *,
        *::before{
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        .main-container{
            background: url(img.jpg) center/cover no-repeat;
            overflow: hidden;
            position: relative;
        }

        .main-container::before{
            content: "";
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.6);
            position: absolute;
            top: 0;
            left: 0;
            z-index: 2;
        }

        .video-container{
            padding-bottom: 56.25%;
        }

        video {
            position: absolute;
            width: 100%;
            height: auto;
            top: 0;
            left: 0;
        }

        .text{
            width: 100%;
            height: 100%;
            position: absolute;
            top: 0;
            left: 0;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: white;
            z-index: 3;
            font-family: sans-serif;
            font-size: 5vw;
        }


        
    </style>
</head>
<body>
    <section class="main-container">
        <div class="video-container">
            <video src="video2.mp4" autoplay loop muted></video>
        </div>
        <div class="text">
            <p>video background</p>
        </div>
    </section>
</body>
</html>
```
