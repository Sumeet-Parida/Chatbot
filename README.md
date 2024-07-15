#!pip install huggingface_hub
#!pip install transformers
#!pip install langchain
#!pip install chainlit

!chainlit hello

import asyncio

async def upload_file():
    while True:
        files = input("Please upload a file (enter the file path): ")
        if files:
            with open(files, 'r') as file:
                text = file.read()
                print(f"File uploaded, it contains {len(text)} characters!")
                break
        else:
            print("No file uploaded. Try again!")

asyncio.run(upload_file())


async def send_messages():
    text_content = "Attention is all you need!"
    elements = [cl.Text(name="Text element!!", content=text_content, display="inline")]
    await cl.Message(content="Check out the text element", elements=elements).send()

    elements = cl.Image(name="Image1", display="inline", path="./image1.jpg")
    await cl.Message(content="Look at this local image", elements=elements).send()

# To run the asynchronous function, you can use the following code:
import asyncio
asyncio.run(send_messages())


import asyncio
import matplotlib.pyplot as plt
import matplotlib.animation as animation
import urllib
import numpy as np

async def display_video():
    video_url = input("Enter the video URL: ")
    fig, ax = plt.subplots()
    ax.axis('off')  # disable axis

    def update(frame):
        img = urllib.request.urlopen(video_url)
        img = np.array(bytearray(img.read()), dtype=np.uint8)
        img = np.reshape(img, (640, 480, 3))  # resize to your video resolution
        ax.imshow(img)
        return ax

    anim = animation.FuncAnimation(fig, update, frames=200, interval=20)
    plt.show()

asyncio.run(display_video())


