### Uncover hidden files

After the tool is finished downloading all the artifacts, run the commands below to recover each of the six secrets I've hidden.

Start by creating the output directory: `out`.

___
**Public and private key pair**

A key pair is in the last 8177 bytes of akamaru.bmp

```
tail -c 8177 akamaru.bmp > out/key_pair.pem
```
___
**Short message listing the pieces of evidence to be found**
```
base64 -di masashi_kishimoto.txt > out/index
```
___
**Map of Area 51, pointing to the aliens' location**
```
python3 stego.py naruto_opening.wav 0 1 out/map
python3 stego.png.py out/map
rm out/map
```
___
**Short message in morse code about the captive aliens**
```
python3 stego.py naruto_scream.wav 0 2 out/a2
python3 stego.wav.py out/a2
rm out/a2
```
___
**SOS morse code sent by the aliens**
```
chmod +x get_sos.sh
./get_sos.sh naruto_run.gif
```
___
**Recording about the leakage of classified information**
```
chmod +x get_word_list.sh
./get_word_list.sh naruto_wikipedia.txt > dict
fcrackzip -uvDp dict villains.zip
```
Write down the password (henceforth designated as `$pwd`).
```
unzip -P $pwd villains.zip
xxd -r -p -o 0 <(echo 4944 3303) momoshiki_otsusuki
mv momoshiki_otsusuki out/audio.mp3
```