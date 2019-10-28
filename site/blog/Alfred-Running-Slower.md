+++
title = "Alfred and Hazel Running Slower"
date = "2018-12-12"
tags = ["alfred", "programming", "zsh", "Hazel"]
categories = ["automation"]
banner = "img/banners/banner-4.jpg"
author = "Richard Guay"
+++
## {{title}}
#### {{cdate date 'MMMM D, YYYY'}}

I love [zsh](http://www.zsh.org/) and [ohmyzsh](https://ohmyz.sh/) for my command line. It looks great and is very flexible. But, I recently added [zplug](https://github.com/zplug/zplug) as well with several great plugins. I would recommend using it. But, you might want to watch out for the "gotcha" that I ran into.

The zplug command runs several checks and loads several scripts each time you load a zsh instance. This does increase the startup time, but I figured that wasn't much of an issue since I load several instances when I boot the system. I then use these shells for all my work during the day.

Around the same time, I started noticing that my [Alfred](https://www.alfredapp.com/) workflows were getting slower. Since I have over 80 workflows and some of them call others, things were getting very slow. At first, I just thought that I was running too many other programs at a time. But, the more I experimented, the more I realized that the scripts were running slower due to the added time of loading a full zsh session.

Alfred started running shell scripts with full, interactive shells instead of the minimum single execution shells. That way, the `.zshrc` file is read where many users were keeping path configurations and many programs are adding their preferences to this file as well. Without loading the `.zshrc` files, many workflows would not work.

I first figured out all the necessary environment variables and made a copy of them in the `.bashrc` file. My bash files only setup a proper running environment for running programs without any fancy command line colorizations, special prompts, etc. I then went through and changed all my workflows to only use bash and not zsh. I also streamlined my `.zshrc` file by putting all configurations needed to run program in the `.zshenv` file and all the interactive shell items in the `.zshrc` file. Zsh is still somewhat slow at first run, but the added benefits of the plugins are worth it.

Now, all of my Alfred workflows run much faster and I have a great interactive shell experience as well. I did the same optimizations for my [Keyboard Maestro](https://www.keyboardmaestro.com/main/) and [Hazel](https://www.noodlesoft.com/) workflows as well.

I hope this tip will help you as much as it has helped me!
