# jupyter_play_video
How to show videos in Jupyter notebooks

```python
def show_video_seq(image_array):
    matplotlib.rcParams['animation.embed_limit'] = 2**128
    dpi = 72.0
    xpixels, ypixels = image_array[0].shape[:2]
    fig = plt.figure(figsize=(ypixels/dpi, xpixels/dpi), dpi=dpi)
    im = plt.figimage(image_array[0])

    def animate(i):
        im.set_array(image_array[i])
        return (im,)

    anim = animation.FuncAnimation(fig, animate, frames=len(image_array), interval=33, repeat_delay=1, repeat=True)
    display(HTML(anim.to_html5_video()))
    

def video2seq(video_path):
    video = cv.VideoCapture(source_video_path)
    seq = []
    while True:
        status, frame = video.read()
        if status is False:
            break
        frame = cv.cvtColor(frame, cv.COLOR_BGR2RGB)
        seq.append(frame)
    video.release()
    return seq
```

```python
source_video_path = "/home/pedro/Downloads/Xiph_videos/720p5994_stockholm_ter.avi"

frames = video2seq(source_video_path)

show_video_seq(frames)
```

Use with moderation.
