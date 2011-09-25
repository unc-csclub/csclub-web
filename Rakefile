require 'nanoc3/tasks'

desc "Compile site, adding static assets"
task :default do
    system 'nanoc3 compile'
    cp_r 'assets/.', 'output'
end
