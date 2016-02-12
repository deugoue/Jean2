# Jean2
Nginx automation
action : create do
# Install nginx using system package resource
# chef-zero
package "#{res_name} : create nginx" do
package_name 'nginx'
action: install
end
create _stop_package_service

## create instance directories
directory "#{re_name} :create/var/log/#{nginx_instance_name}" do
path "/var/log/#{nginx_instance_name}"
owner new_resource.run_user
group 'adm'
mode 00755
action :create
end

%W(
/etc/#{nginx_instance_name}
/etc/#{nginx_instance_name}/conf.d
/etc/#{nginx_instance_name}/sites-available
/etc/#{nginx_instance_name}sites-enabled
).each do |instance_dir|
directory"#{res_name} :create #{instance_dir}" do
path instance_dir
owner 'root'
group 'root'
mode 00755
action :create
end
end
