FROM ianpurton/rust-slim-devcontainer:latest AS development

# Configure apt and install packages
RUN sudo apt-get update \
    && sudo apt-get install -y --no-install-recommends \
        postgresql-client \
    # Clean up
    && sudo apt-get autoremove -y \
    && sudo apt-get clean -y \
    && sudo rm -r /var/cache/* /var/lib/apt/lists/*

# My git aliases
RUN echo "alias gst='git status'"  >> ~/.bashrc \ 
    && echo "alias gcm='git checkout master'"  >> ~/.bashrc \  
    && echo "alias c=clear"  >> ~/.bashrc \  
    && echo "alias gp='git push'"  >> ~/.bashrc \  
    && echo "alias gcam='git commit -a -m'"  >> ~/.bashrc \  
    && echo "alias gpsup='git push --set-upstream origin $(git_current_branch)'"  >> ~/.bashrc \  
    && echo "alias gcb='git checkout -b'" >> ~/.bashrc \
    && echo "alias gitsetup='git config --global user.name \$NAME && git config --global user.email \$EMAIL && mkdir -p ~/.ssh && cp -u /home/host-ssh/id_rsa ~/.ssh && chmod 600 ~/.ssh/id_rsa && ssh-keygen -y -f ~/.ssh/id_rsa > ~/.ssh/id_rsa.pub'" >> ~/.bashrc

# Looks like migration is not compatible with immudb (Find another one)
RUN echo "alias migration='docker run --network host -v \$HPWD/migrations:/usr/src/migrations -it --rm -e DATABASE_URL=\$MIGRATIONS_DATABASE_URL ianpurton/rust-diesel diesel migration'" >> ~/.bashrc

# Code Notary VCN
RUN curl http://getvcn.codenotary.io -L | sh