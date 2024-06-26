# My JITL CCNA's Notes

## Main Contents:

#### [Free CCNA 200-301 | Complete Course 2023](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ) The main videos being used to make notes.
#### [JeremyITLab Official Website](https://courses.jeremysitlab.com/) His official website.

### Requirements:
* ##### [Pandoc Mermaid-Filter (GitHub)](https://github.com/raghur/mermaid-filter)
	* Used to render Mermaid diagram in pdf/latex.
* ##### Pandoc extension CLI Argument:

```shell
--highlight-style tango --filter mermaid-filter.cmd -V geometry:top=0.5in -V author:Purinat33 -V fontsize=12pt -V linestretch=1.2 -V papersize=a4
```

* Pandoc setting
	![[img/README-5.png]]
* ##### [PDFLaTex (Installed with TexLive)](https://tug.org/texlive/windows.html#install)
* CSS Snippet (style.css) in `.obsidian/snippets` folder:

```css
img[alt*="center"] {
    display: block;
    margin-left: auto;
    margin-right: auto;
}
```

## Extra contents I used/planned on using:

![](img/README.jpg)
#### [CCNA Official Cert Guide Library via ciscopress.com](https://www.ciscopress.com/store/ccna-200-301-official-cert-guide-library-9781587147142)

![](img/README-1.png)
#### [Practical Networking by Ed Harmoush](https://www.practicalnetworking.net/)

![](img/README.webp)
#### [Neil Anderson's CCNA Lab Guide (Free)](https://www.flackbox.com/cisco-ccna-lab-guide)

![](img/README-2.png)

#### [Wendell Odom's CertSkills (Official Cert Guide's author)](https://www.certskills.com/)

![](img/README-3.png)
#### [The Keith Barker's Packet Tracer Lab](https://www.thekeithbarker.com/)

Big thank  you to Jeremy and others for providing easy-to-understand Networking and CCNA knowledge for learners, including me.  

<hr>

## Tools used:
* Obsidian Text editor
	1. **Plugin**:
		* Editor Syntax Highlight
		* Excalidraw
		* Git
		* Mermaid Tool
		* Pandoc
		* Paste Image Rename
			* Handle All Attachments: **true**
			* Exclude patterns: **err**
	2. **Setting**:
		![](img/README-4.png)