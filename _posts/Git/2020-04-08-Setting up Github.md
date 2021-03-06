---
layout: post
title: Setting up Github
comments: true
categories: Git
---

## GitHub Initial Setting<br>
[GitHub SSH key setting 참고 Link](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)

### [Generating a new SSH key and adding it to the ssh-agent]<br>

홈페이지의 Instruction을 따라서 SSH키를 generate한 뒤에, 개인 GitHub 계정에 setting해본다.<br>

    hyungilee@HYUNGIs-MacBook-Pro ~ % ssh-keygen -t rsa -b 4096 -C "mike.hyungi.lee@gmail.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key (/Users/hyungilee/.ssh/id_rsa):
    Created directory '/Users/hyungilee/.ssh'.
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in /Users/hyungilee/.ssh/id_rsa.
    Your public key has been saved in /Users/hyungilee/.ssh/id_rsa.pub.
    The key fingerprint is:
    SHA256:mNbD+8ugZkiabHbAxHz80dw8I++O9O0gRDtjrGEMqEs mike.hyungi.lee@gmail.com
    The key's randomart image is:
    +---[RSA 4096]----+
    |                 |
    |   .             |
    | o...  o.o       |
    | .+ oo.B+.=      |
    |.E . .B.So o     |
    |..o .o.= =.      |
    |.. = .. =..      |
    |  * o oo B.o     |
    | o . o. ..*oo    |
    +----[SHA256]-----+
    hyungilee@HYUNGIs-MacBook-Pro ~ % eval "$(ssh-agent -s)"
    Agent pid 5969

    hyungilee@HYUNGIs-MacBook-Pro .ssh % cat ./config
    Host *
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_rsa
    hyungilee@HYUNGIs-MacBook-Pro .ssh % pwd
    /Users/hyungilee/.ssh
    hyungilee@HYUNGIs-MacBook-Pro .ssh % ssh-add -K ~/.ssh/id_rsa
    Identity added: /Users/hyungilee/.ssh/id_rsa (mike.hyungi.lee@gmail.com)

### [Adding a new SSH key to your GitHub account]

    hyungilee@HYUNGIs-MacBook-Pro .ssh % pbcopy < ~/.ssh/id_rsa.pub

생성된 SSH키를 클립보드에 복사한 후에, GitHub계정의 SSH keys Setting에 붙여넣고, 추가해준다.
<img src="/images/android/2020-04-08 Add SSH Key into GitHub setting.png" alt="blog capture" width="500" title="capture img">
