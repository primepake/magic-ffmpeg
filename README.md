- video to frames: `ffmpeg -i video.mp4 'outputs/%05d.jpg'`
- convert to fps=20: `ffmpeg -y -i background.mp4 -filter:v fps=fps=20 20fps.mp4`
- change frame rate: `ffmpeg -i 1.mp4 -filter:v fps=fps=25 1_25.mp4`
- frams to video: `ffmpeg -framerate 20 -pattern_type glob -i 'outputs/*.jpg' -c:v libx264 -pix_fmt yuv420p out.mp4`
- overlay video to image: `ffmpeg -loop 1 -i background.jpg -i 1_25.mp4 -filter_complex "overlay=(W-w)/2:shortest=1" output.mp4`
- crop video: `ffmpeg -i temp_download_video.mp4 -ss t1 -to t2 temp.mp4`
- concate video: `ffmpeg -f concat -safe 0 -i cat.txt -c copy output.mp4`

20-46

- extract audio from video: `ffmpeg -i in.mp4 -vn -ac 2 out.mp3`
- merge audio and video: `ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac output.mp4`
- images to webm: `ffmpeg -framerate 20 -i frames/%03d.png output.webm`
- webm + background image: `ffmpeg -loop 1 -i background.jpg -i output.webm -filter_complex "overlay=(W-w)/2:shortest=1" temp.mp4`
- padding for video: `ffmpeg -i santa.webm -filter_complex "pad=1920:1080:(ow-iw)/2:(oh-ih)/2" output.webm`
- add video with audio (auto repeat video): `ffmpeg -stream_loop -1 -i input.mp4 -i input.mp3 -shortest -map 0:v:0 -map 1:a:0 -y out.mp4`
- webm + background image: `ffmpeg -c:v libvpx-vp9 -i `output`.webm -i `backgroun`d.jpg -filter_complex "[1:v][0:v] overlay=25:25:enable='between(t,0,20)'" -pix_fmt yuv420p -c:a copy output_trans.mp4`
- webm + video background: `ffmpeg -i santa_cropped.mp4 -c:v libvpx-vp9 -i output.webm -filter_complex overlay output.mp4`
- overlay image to video background: `ffmpeg -i background.mp4 -i image.png -filter_complex "[0:v][1:v] overlay=500:200" -pix_fmt yuv420p -c:a copy test.mp4`
- overlay image with scale to video background: `ffmpeg -i 01.mp4 -i transparent.png -filter_complex "[1]scale=iw*0.7:-1[wm];[0][wm]overlay=x=(W-w)/2:y=(H-h)/2" -pix_fmt yuv420p -c:a copy test.mp4`
- gif to mp4: `ffmpeg -i 03.gif -pix_fmt yuv420p 03.mp4`
- overlay video on video: `ffmpeg -i bg.mp4 -i fg.mkv -filter_complex "[0:v][1:v]overlay=enable='between=(t,10,20)':x=720+t*28:y=t*10[out]" -map "[out]" output.mkv`

- overlay cycle video on video background: `ffmpeg -y -i background.mp4 -i res.mp4 -filter_complex \
"[1]format=yuva444p,geq=lum='p(X,Y)':a='st(1,pow(min(W/2,H/2),2))+st(3,pow(X-(W/2),2)+pow(Y-(H/2),2));if(lte(ld(3),ld(1)),255,0)'[circular shaped video];[circular shaped video]scale=640:-1[ovrl],[0:v][ovrl]overlay=enable='between=(t,0,10)':x=1500:y=800[out]" \
-map "[out]" output.mp4`

- overlay cycle video on image background: `ffmpeg -y -i background_1920x1080.jpeg -i mia.mp4 -filter_complex "[1]format=yuva444p,geq=lum='p(X,Y)':a='st(1,pow(min(W/2,H/2),2))+st(3,pow(X-(W/2),2)+pow(Y-(H/2),2));if(lte(ld(3),ld(1)),255,0)'[circular shaped video];[circular shaped video]scale=-1:540[ovrl],[0:v][ovrl]overlay=500:500[out]" -map "[out]" output_rv.mp4`

- overlay image on image: `ffmpeg -y -i background.png -i image.png -filter_complex '[1]scale=960:-1[wm];[0][wm]overlay=x=537.6:y=486' -pix_fmt yuv420p -c:a copy temp.jpg`

- extract mp3: `ffmpeg -i video.mp4 -vn -ac 2 audio.mp3`

- merge 2 audio with video:`ffmpeg -y -i video.mp4 -i audio1.mp3 -i audio2.mp3 -filter_complex "[1][2]amix=inputs=2[a]" -map 0:v -map "[a]" -c:v copy video_output.mp4`

- scale video: `ffmpeg -i input.avi -filter:v scale=720:-1 -c:a copy output.mkv`