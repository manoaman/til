### Apple

#### How to show hidden files?

1. Open Terminal found in Finder > Applications > Utilities.
2. In Terminal, paste the following: defaults write com.apple.finder AppleShowAllFiles YES.
3. Press return.
4. Hold the 'Option/alt' key, then right click on the Finder icon in the dock and click Relaunch.

#### How to upgrade chromedriver?

```
% npm install chromedriver
% sudo ln -s /Users/seita/node_modules/chromedriver/lib/chromedriver/chromedriver /usr/local/bin/chromedriver
% /usr/local/bin/chromedriver -version
ChromeDriver 74.0.3729.6 (255758eccf3d244491b8a1317aa76e1ce10d57e9-refs/branch-heads/3729@{#29})
```
https://www.kenst.com/2015/03/installing-chromedriver-on-mac-osx/

#### How to diagnose WiFi connection on Mac?

`alt + (click on the WiFi menu)`

https://support.apple.com/en-us/HT202663#howto


#### How to count CPU cores and RAM size from terminal?

```
% sysctl -n hw.ncpu
4

% sysctl hw.memsize
hw.memsize: 8589934592

```

https://serverfault.com/questions/112711/how-can-i-get-cpu-count-and-total-ram-from-the-os-x-command-line
