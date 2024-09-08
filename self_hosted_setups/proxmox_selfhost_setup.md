# After Installation
$${\color{orange}1.}$$ Select Host

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

${\color{orange}11.}$ Select Updates > Refresh wait for it to finish then `>_Upgrade`


# [STORAGE](https://technotim.live/posts/first-11-things-proxmox/#storage)
Author: [TechnoTim](https://technotim.live/posts/first-11-things-proxmox/)

## Create ZFS

${\color{orange}1.}$ SSH into your ProxMox or use `>_Shell`

${\color{orange}2.}$ Type fdisk /dev/sd**X** - ${\color{red}where\space \color{white}X\space \color{red}define\space the\space letter\space of\space the\space drive\space you\space want\space to\space clear.}$
 - ${\color{orange}2a.}$ Use ${\color{yellow}P\space \color{white}for Partition.}$
 - ${\color{orange}2b.}$ Use ${\color{yellow}D\space \color{white}for Delete.}$
 - ${\color{orange}2c.}$ Select the number of the partition you want to delete i.e (1,2,3, etc)
 - ${\color{orange}2d.}$ Use ${\color{yellow}P\space \color{white}for\space Partition\space again\space to\space check\space the\space Partitions.}$
 - ${\color{orange}2e.}$ Use ${\color{yellow}W\space \color{white}for\space updating\space the\space Partition\space Table.}$
 - ${\color{orange}2f.}$ Use ${\color{yellow}Q\space \color{white}for\space quitting\space the\space FDISK \space (if needed).}$

 - $${\color{orange}2a.}$$ Use $${\color{yellow}P}$$ for Partition.

# [Removing ProxMox Subscription Notice](https://www.reddit.com/r/Proxmox/comments/tgojp1/removing_proxmox_subscription_notice/)
Author: [Roaster-Dude](https://www.reddit.com/user/Roaster-Dude/)

Original directions are from John's Computer Services but when I did this mod my refresh button stopped refreshing the package listing.
So I dug to see it I could tell why and discovered it was pretty easy to change it.

To remove the **“You do not have a valid subscription for this server”** popup message while logging in and when refreshing packages to do updates.

$${\color{orange}1.}$$ Login to your host either via SSH or via the >_Shell in your Browser
> [!NOTE]
> If you use the **>_Shell** option note that **Ctrl-W** to search in nano might close the tab in your browser if that happens better use an SSH client.

$${\color{orange}2.}$$ Navigate to 

```sh
	cd /usr/share/javascript/proxmox-widget-toolkit
```

$${\color{orange}3.}$$ Make a backup 
```sh
	cp proxmoxlib.js proxmoxlib.js.bak
```

$${\color{orange}4.}$$ Edit the file 
```sh
	nano proxmoxlib.js
```

$${\color{orange}5.}$$ Use ***Ctrl-W*** to search for **"No valid subscription"**

```javascript
	.data.status.toLowerCase() !== 'active') {
		Ext.Msg.show({
			title: gettext('No valid subscription'),
```

$${\color{orange}6.}$$ Remove the **!** before the **==**

$${\color{orange}7.}$$ It should now look like the code below

```javascript
	.data.status.toLowerCase() == 'active') {
```

$${\color{orange}8.}$$ **Ctrl-O** to save the file **Ctrl-X** to exit NANO.

$${\color{orange}9.}$$ Restart the ProxMox service.

```sh
	systemctl restart pveproxy.service
```

$${\color{orange}10.}$$ Reload your browser tab and log back in if needed.

> [!TIP]
> This just changes the logic of the code from not active to active.

> [!IMPORTANT]
> Please support the Proxmox team by [buying a subscription](https://www.proxmox.com/en/proxmox-ve/pricing) if it's within your means. High quality open source software like Proxmox needs our support!. ***If you pay for a subscription then you would need to change it back.***