### SSH stuffs

#### SSH login without password?

1. First log in on A as user a and generate a pair of authentication keys.
```
% ssh-keygen -t rsa
```

2. Now use ssh to create a directory ~/.ssh as user b on B. (The directory may already exist, which is fine)
```
% ssh hogeuser@hogehoge.com mkdir -p .ssh
```

3. Finally append a's new public key to b@B:.ssh/authorized_keys and enter b's password one last time
```
% cat .ssh/id_rsa.pub | ssh hogeuser@hogehoge.com 'cat >> .ssh/authorized_keys'
```

And it should work without password prompt.

http://www.linuxproblem.org/art_9.html
