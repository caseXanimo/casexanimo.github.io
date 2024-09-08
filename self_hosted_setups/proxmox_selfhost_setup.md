# After Installation

```html
1. <span style="color: orange;">Select Host</span>
```

$${\color{orange}2.}$$ Go to **Updates** > **Repositories**

$${\color{orange}3.}$$ Disable Enterprise repositories (both or more if any)

$${\color{orange}4.}$$ Click on **ADD**

$${\color{orange}5.}$$ Select from the drop down list **No-Subscription**

$${\color{orange}6.}$$ Click **ADD**

$${\color{orange}7.}$$ Either from the ***>_Shell*** or ***SSH*** into your host go to directory 

```sh
	/etc/apt/sources.list
```

$${\color{orange}8.}$$ Correct the existing entry as below

```
	# non-production updates (unstable) 
	deb http://download.proxmox.com/debian bookworm 
```

$${\color{orange}9.}$$ Ctrl+S to Save the file.

$${\color{orange}10.}$$ Reload from your GUI to see the changes.

$${\color{orange}11.}$$ Select Updates > Refresh wait for it to finish then >_Upgrade