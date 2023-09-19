# ServidorFTP_UBUNTU
Servidor FTP em Ubuntu


<h2>Instale o vsftpd:</h2>

Certifique-se de que seu sistema esteja atualizado e, em seguida, instale o vsftpd usando o comando:

<b>sudo apt update
sudo apt install vsftpd</b>


Configurar o vsftpd:

Abra o arquivo de configuração do vsftpd para edição com o seguinte comando:


sudo nano /etc/vsftpd.conf


Dentro do arquivo, certifique-se de que as seguintes linhas estejam configuradas:

anonymous_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
Essas configurações desabilitam o acesso anônimo, permitem o acesso local, habilitam a gravação de arquivos e impõem o chroot para que os usuários fiquem confinados às suas próprias pastas.

<h2>Crie as contas de usuário:</h2>


sudo adduser nome_de_usuario
Depois de criar os usuários, configure as senhas usando:

sudo passwd nome_de_usuario


Defina permissões para a pasta "projeto":

Supondo que a pasta "projeto" esteja localizada em /var/ftp, você pode configurar as permissões da seguinte forma:


sudo chown -R root:nome_de_usuario /var/ftp/projeto
sudo chmod -R 770 /var/ftp/projeto
Substitua "nome_de_usuario" pelo nome de cada usuário que precisa de acesso total à pasta "projeto".



<h2>Reinicie o vsftpd:</h2>

Após fazer todas as configurações, reinicie o serviço vsftpd para aplicar as alterações:

sudo systemctl restart vsftpd

<h2>Caso precise que todos os usuarios acessem a mesma pasta</h2>

Defina permissões no diretório home:

Você deve definir as permissões corretas no diretório home do usuário "nome_de_usuario" para que ele possa acessá-lo:


sudo chown nome_de_usuario:nome_de_usuario /home/nome_de_usuario
sudo chmod 755 /home/nome_de_usuario

Crie um link simbólico para a pasta "projeto":

Agora, você pode criar um link simbólico na pasta home do usuário "nome_de_usuario" que aponta para a pasta "projeto":


ln -s /var/ftp/projeto /home/nome_de_usuario/projeto

Atualize as configurações do vsftpd:

Edite o arquivo de configuração do vsftpd novamente:
sudo nano /etc/vsftpd.conf


Certifique-se de que a linha chroot_local_user esteja definida como YES.

chroot_local_user=YES



Reinicie o serviço vsftpd para aplicar as alterações:

sudo systemctl restart vsftpd
