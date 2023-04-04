# ����OpenStack����NestOS

��ָ��չʾ�������OpenStackƽ̨�ϲ���NestOS��

ĿǰNestOS֧��x86_64��aarch64���ּܹ���

### ��ʼ֮ǰ

�6�7		�ڿ�ʼ���� NestOS ֮ǰ,��Ҫ������׼������:

- ���� NestOS OpenStack qcow2
- ׼�� config.bu �ļ�
- ���� butane ����(Linux����/win10����)
- OpenStackƽ̨

### ���� ignition �ļ�

#### ��ȡ Butane

����ͨ�� Butane �� bu �ļ�ת��Ϊ igniton �ļ���ignition �����ļ������Ϊ�ɶ������Ա�д����Ϊ��
��ֹ�û������ֶ���д���á�
Butane �ṩ�˶��ֻ�����֧�֣������� linux/windows �������л����������н������á�

```
docker pull hub.oepkgs.net/nestos/butane:0.14.0
```

#### ���ɵ�¼����

��������ִ���������������������롣

```
# openssl passwd -1 -salt yoursalt
Password:
$1$yoursalt$1QskegeyhtMG2tdh0ldQN0
```

#### ����ssh-key

��������ִ�����������ȡ��Կ��˽Կ�Թ����� ssh ��¼��

```
# ssh-keygen -N '' -f ./id_rsa
Generating public/private rsa key pair.
Your identification has been saved in ./id_rsa
Your public key has been saved in ./id_rsa.pub
The key fingerprint is:
SHA256:4fFpDDyGHOYEd2fPaprKvvqst3T1xBQuk3mbdon+0Xs root@host-12-0-0-141
```

```
The key's randomart image is:
+---[RSA 3072]----+
|   ..= . o .   |
|    * = o * .  |
|     + B = *   |
|     o B O + . |
|      S O B o  |
|       * = . . |
|      . +o . . |
|     +.o . .E  |
|    o*Oo   ... |
+----[SHA256]-----+
```

�����ڵ�ǰĿ¼�鿴id_rsa.pub��Կ

```
# cat id_rsa.pub
ssh-rsa
AAAAB3NzaC1yc2EAAAADAQABAAABgQDjf+I9QQZ+3vNWomqxpHkZq7ONHcEYBzs4C9RZahmLYVPBf/3y
HF5wTtfl5CBviERUnLGFn8c4Ua9MNWcJL6zE01xXtDZ2db7vaPwP3Qbo1lKJg1BVw6u+5bMKCJxEnN9+
aOiX3A2XpkUVxhCoGlei3j78oLRU3ucCLn6m7wVE+P53tNQ5364xWqbAsDXdze4xnNZjlzH9JvjJ5IJY
WjwrD7UUkfI8qDj5ub9Gz+nSenaaSboWADsKe4JTLoU2Gz5fPLCj+uuNFpZAUc/GCe47He5UO6IbHjDI
bxqhzYZQTXdwIgKIM1PL19IkAAY07gU53b4gDSDj7SZYB+jjtgG8VoFF4m7nCJgRDeUKGTNT5fsLPKAZ
tmBvy9Mg5qkK/LisEzjUwPPh1NEb8bgN251wPXmPMjQ1aMzD8t9blq40KEyod2Eg05nW2q5/90ICNQBa
r9AkQrQ/3j8WsejvqseWIi1kq68pqvtcBJkCMiIfzIoUgCgcolw3fZprDhgfau8= root@host-12-0-
0-141
```

#### ��дbu�ļ�

������򵥵ĳ�ʼ���ã����������ϸ�����ã��ο������ ignition ��⡣
����Ϊ��򵥵� config.bu �ļ�

```
variant: nestos
version: 1.1.0
passwd:
  users:
    - name: core
      password_hash: "$1$yoursalt$1QskegeyhtMG2tdh0ldQN0"
      ssh_authorized_keys:
        - "ssh-rsa
  AAAAB3NzaC1yc2EAAAADAQABAAABgQDjf+I9QQZ+3vNWomqxpHkZq7ONHcEYBzs4C9RZahmLYVPBf/3y
  HF5wTtfl5CBviERUnLGFn8c4Ua9MNWcJL6zE01xXtDZ2db7vaPwP3Qbo1lKJg1BVw6u+5bMKCJxEnN9+
  aOiX3A2XpkUVxhCoGlei3j78oLRU3ucCLn6m7wVE+P53tNQ5364xWqbAsDXdze4xnNZjlzH9JvjJ5IJY
  WjwrD7UUkfI8qDj5ub9Gz+nSenaaSboWADsKe4JTLoU2Gz5fPLCj+uuNFpZAUc/GCe47He5UO6IbHjDI
  bxqhzYZQTXdwIgKIM1PL19IkAAY07gU53b4gDSDj7SZYB+jjtgG8VoFF4m7nCJgRDeUKGTNT5fsLPKAZ
  tmBvy9Mg5qkK/LisEzjUwPPh1NEb8bgN251wPXmPMjQ1aMzD8t9blq40KEyod2Eg05nW2q5/90ICNQBa
  r9AkQrQ/3j8WsejvqseWIi1kq68pqvtcBJkCMiIfzIoUgCgcolw3fZprDhgfau8= root@host-12-0-
  0-141"
```

#### ����ignition�ļ�

�� config.bu ͨ�� Butane ����ת��Ϊ config.ign �ļ�������Ϊ�����������½���ת����

```
# docker run --interactive --rm hub.oepkgs.net/nestos/butane:0.14.0 \
--pretty --strict < your_config.bu > config.ign
```

Ҳ�������������½���ת����Butane�ṩ�˶���ת���ķ�ʽ,�������µ�ַ�鿴��
https://github.com/coreos/butane

### ��װ���� NestOS

��OpenStackƽ̨���ϴ� NestOS OpenStack qcow2����

```
openstack image create --disk-format=qcow2 --min-disk=10 --min-ram=2 --file=nestos nestos-XX.XXXXXXXX.X.X-openstack.x86_64.qcow2
```

�����ϴ��ɹ�������NestOSʵ��

```
openstack server create            \
     --key-name=mykeypair          \
     --network=private             \
     --flavor=v1-standard-2        \
     --image=nestos                \
     --user-data config.ign.ign    \
     nestos-openstack
```
����ִ�гɹ��ɳɹ�����NestOSʵ��