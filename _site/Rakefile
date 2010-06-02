require 'rubygems'
require 'highline/import'
require 'net/ssh'

GITHUB_REPO = 'git://github.com/lucasefe/www.justoalcaer.com.ar.git'
PRODUCTION = 'neura.lucasefe.com.ar:/var/apps/www.lucasefe.com.ar/'

desc "deploy site to litanyagainstfear.com"
task :deploy do
  deploy_to(PRODUCTION)  
end
task :setup do
  cold_deploy_to(PRODUCTION, GITHUB_REPO)
end

def cold_deploy_to(to, from)
  username, password = fetch_credentials
  host, dir = to.split(":")
  deploy_dir = "#{dir}/cached-copy"
  
  Net::SSH.start(host, username, :port => 22, :password => password) do |ssh|
    commands = <<-EOF
      mkdir -p #{deploy_dir}
      cd #{deploy_dir}
      git clone #{from} .
    EOF
    commands = commands.gsub(/\n/, "; ")
    ssh.exec commands
  end
end
def deploy_to(to)
  username, password = fetch_credentials
  host, dir = to.split(":")
  deploy_dir = "#{dir}/cached-copy"
  Net::SSH.start(host, username, :port => 22, :password => password) do |ssh|
    commands = <<-EOF
      cd #{deploy_dir}
      git pull
    EOF
    commands = commands.gsub(/\n/, "; ")
    ssh.exec commands    
  end
end
def fetch_credentials
  username = ask("Username: ") { |q| q.echo = true }
  password = ask("Password: ") { |q| q.echo = "*" }
  return username, password
end