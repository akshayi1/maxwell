#!/usr/bin/env ruby
require 'zendesk/deployment'

set :application, 'zendesk_exodus_binlog_service'
set :repository, 'git@github.com:/zendesk/exodus_binlog_service.git'
set :config_files, %w(exodus_binlog_service.yml)

namespace :deploy do
  task :restart do
    run "sudo sv restart /etc/service/binlog_service"
  end

  task :configure do
    config_files.each do |file|
      run "ln -nfs #{deploy_to}/config/#{file} #{release_path}/config/"
    end

    run <<-SCRIPT
      rm -rf #{release_path}/data && ln -nfs #{deploy_to}/data #{release_path}/data
    SCRIPT
  end

  task :stop do
  end

  task :start do
  end
end

after 'deploy:update_code', 'deploy:configure'
