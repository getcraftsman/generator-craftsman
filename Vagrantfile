require "json"
require "yaml"

VAGRANTFILE_API_VERSION ||= "2"

craftsmanYamlPath = "Craftsman.yaml"
craftsmanJsonPath = "Craftsman.json"
afterScriptPath = "after.sh"
aliasesPath = "aliases"

require File.expand_path("scripts/craftsman.rb")

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    if File.exist? aliasesPath then
        config.vm.provision "file", source: aliasesPath, destination: "~/.bash_aliases"
    end

    if File.exist? craftsmanYamlPath then
        Craftsman.configure(config, YAML::load(File.read(craftsmanYamlPath)))
    elsif File.exist? craftsmanJsonPath then
        Craftsman.configure(config, JSON.parse(File.read(craftsmanJsonPath)))
    end

    if File.exist? afterScriptPath then
        config.vm.provision "shell", path: afterScriptPath
    end
end
