# python-video-player
this is a code for a video player in python that lets u play,pause the video ,increase,decrese the volume and rewind back to the start of the video 

    import cv2
    import numpy as np
    #ffpyplayer for playing audio
    from pymediainfo import MediaInfo
    from ffpyplayer.player import MediaPlayer
    video_path="video.mp4"
    def PlayVideo(video_path):
    video=cv2.VideoCapture(video_path)
    player = MediaPlayer(video_path)
    while True:
        grabbed, frame=video.read()
        audio_frame, val = player.get_frame()
        frame=cv2.resize(frame,(700,600))
        if not grabbed:
            print("End of video")
            break
        key=cv2.waitKey(29)
        if key==27:
            player.close_player()
            break
        if key==ord("h"):
            player.set_volume(1.0)
        if key==ord("l"):
            player.set_volume(0.0)
        if key==32:
            player.toggle_pause()
            cv2.waitKey()
            player.toggle_pause()
        cv2.imshow("Video", frame)
        if val != 'eof' and audio_frame is not None:
            #audio
            img, t = audio_frame
    video.release()
    cv2.destroyAllWindows()

    PlayVideo(video_path)
