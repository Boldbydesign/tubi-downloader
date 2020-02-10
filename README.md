### [TubiTV Downloader](https://github.com/warren-bank/node-hls-downloader-tubitv)

Command-line utility for downloading an offline copy of [TubiTV](https://tubitv.com/) HLS video streams.

#### Installation:

```bash
npm install --global @warren-bank/node-hls-downloader-tubitv
```

#### Features:

* accepts URLs that identify:
  - a single movie
  - a single episode contained in a series
  - an entire series
    * includes all episodes in every seasons
* downloads:
  - the highest available quality for each video stream
  - _.srt_ subtitles for all available languages
  - will continue upon restart after an abrupt interruption
* resulting file structure:
  ```bash
    |- {title_series}/
    |  |- {title_episode}/
    |  |  |- hls/
    |  |  |  |- video/
    |  |  |  |  |- *.ts
    |  |  |  |- audio/
    |  |  |  |  |- {language}/
    |  |  |  |  |  |- *.ts
    |  |  |  |  |- {language}.m3u8
    |  |  |  |- subtitles/
    |  |  |  |  |- {language}/
    |  |  |  |  |  |- *.vtt
    |  |  |  |  |- {language}.m3u8
    |  |  |  |- video.m3u8
    |  |  |  |- master.m3u8
    |  |  |- mp4/
    |  |  |  |- video.mp4
    |  |  |  |- video.{language}.srt
  ```

#### Usage:

```bash
tubidl <options>

options:
========
"-h"
"--help"
    Print a help message describing all command-line options.

"-V"
"--version"
    Display the version.

"-u" <URL>
"--url" <URL>
    Specify the URL of master manifest.

"-nm"
"--no-mp4"
    Do not use "ffmpeg" to bundle the downloaded video stream into an .mp4 file container.

"-mc" <integer>
"--max-concurrency" <integer>
"--threads" <integer>
    Specify the maximum number of URLs to download in parallel.
    The default is 1, which processes the download queue sequentially.

"-P" <dirpath>
"--directory-prefix" <dirpath>
    Specifies the directory where the resulting file structure will be saved to.
    The default is "." (the current directory).
```

#### Example:

* a movie:
  ```bash
    tubidl -mc 5 -u 'https://tubitv.com/movies/465487/citizenfour'
  ```
* an episode:
  ```bash
    tubidl -mc 5 -u 'https://tubitv.com/tv-shows/498780/s01_e02_the_grand_deception_part_2'
  ```
* a series:
  ```bash
    tubidl -mc 5 -u 'https://tubitv.com/series/4068/the_greatest_american_hero'
  ```

#### Requirements:

* Node version: v6.13.0 (and higher)
  * [ES6 support](http://node.green/)
    * v0.12.18+: Promise
    * v4.08.03+: Object shorthand methods
    * v5.12.00+: spread operator
    * v6.04.00+: Proxy constructor
    * v6.04.00+: Proxy 'apply' handler
    * v6.04.00+: Reflect.apply
  * [URL](https://nodejs.org/api/url.html)
    * v6.13.00+: [Browser-compatible URL class](https://nodejs.org/api/url.html#url_class_url)
  * tested in:
    * v7.9.0
* FFmpeg
  * not required in `PATH` when using the `--no-mp4` CLI option
  * successfully tested with version: _4.1.3_

#### Legal:

* copyright: [Warren Bank](https://github.com/warren-bank)
* license: [GPL-2.0](https://www.gnu.org/licenses/old-licenses/gpl-2.0.txt)
