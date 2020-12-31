# ssl-nginx-aws
ssl nginx aws linux ami 2

    sudo yum install -y certbot python2-certbot-nginx
    sudo certbot -h
    sudo certbot [SUBCOMMAND] [options] [-d DOMAIN] [-d DOMAIN]
    sudo certbot --nginx -d example.com

   > Note: If above step does not work for amazon linux 2 follow bellow step
   > clone git repo: git clone https://github.com/certbot/certbot
   > install python3
   > go to environment of python: source venv3/bin/activate
   > sudo su
   > source venv3/bin/activate lần 2
   > run certbot, then do follow instruction
   > https://certbot.eff.org/docs/contributing.html
    
 ##### reference
 https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/SSL-on-amazon-linux-2.html#letsencrypt
 
