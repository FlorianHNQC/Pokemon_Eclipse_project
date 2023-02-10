"Cartographer" Alpha v1.2.7 - A procedural RMXP map generation tool.

Included Files:
CartographerAlpha.jar			-This is the executable program
CartographerOutput			-The generated PBS (encounters, connections, metadata, and townmap) will be placed here, as well as mapinfos.yaml.
						*Folder will be generated when the program outputs map files.
YAML					-The .yaml files for each map will go here. Rvpacker will also unpack files to this folder.
						*Folder will be generated when the program outputs map files.
CartographerConfig			-This folder will contain any other files needed for Cartographer to run that are not part of the RMXP project.
	>README.txt			-(this file)
	>biomes.txt			-This file is used to determine which pokemon can be placed in each biome type. A default config with mostly generation I
					pokemon is provided, but this file can be customized - see the top of the file for more info.
	>trainertypesconfig.txt		-This file is used to determine which Trainer Types can be generated and how they should be treated. It works in tandem
					with the trainertypes.txt in your PBS folder as well as the files in Cartogropher's "trainerpokemon" folder.
	>malenames/femalenames.txt	-These files are a simple list of names which are used for randomly generated trainers.
	>TrainerPokemon			-This folder contains individual files for each trainer class listing what pokemon they can have at what levels. These
					files are configured in a similar way as the biomes.txt
Data					-This folder should be merged with your RMXP project folder.
	>Tilesets.rxdata		-This is the custom tileset used for this tool. Note that it will replace ANY existing tileset data, so it's recommended
					to do this on a fresh Essentials project.
Graphics\Tilesets			-This folder + subfolder contains the PNG image for the tileset. It can be merged with your project folders without conflict. 
	>OutsideCartographer.png	-This is the custom tileset's image. It is very similar to the default tileset with a few additions.
Graphics\Pictures			-This folder is where the worldmap.png file used for the Town Map will be generated. The folder will already exist in your RMXP project.

Requirements
------------------------------------------------------------------------------------------------------------------------

In order to run CartographerAlpha.jar, you will need Java installed. It is available here:
https://www.java.com/en/download/

In order to convert .rxdata files into .yaml and vice versa, you will need a converter tool.
I used a Ruby gem called rvpacker. In order to use this, you will first need Ruby. 
Windows users can get it here:
https://rubyinstaller.org/

After Ruby is installed you can install the rvpacker gem, and it's dependency gem called scanf.
Cartographer provides a button which will install these gems once you have manually installed Ruby.

If you prefer to use the command line, you can run:

gem install scanf
gem install rvpacker

Further documentation about rvpacker can be found here:
https://github.com/Solistra/rvpacker
Or here:
https://www.rubydoc.info/gems/rvpacker/1.2.0

How to use this program
------------------------------------------------------------------------------------------------------------------------
You should first install Java and Ruby using the above links.

After unzipping CartographerAlpha, copy and paste the entire contents into a fresh Essentials project. Merge any folders
if prompted. Note that tilesets.rxdata WILL be overwritten, which would overwrite any prexisting custom tilesets.

The following steps will be needed to generate a region and import it into RMXP:
	1. Run CartographerAlpha.jar
	2. Click "Install RVPacker" if you have not done so already. This will fail if Ruby is not installed first.
	3. You will need to "Unpack" your project into YAML files - so click the "Unpack" button. (requires RVPacker to be
		installed) You should see a YAML folder appear in your project with several files. We'll come back to that later.
	4. Choose your generation options. More info about the options is described below.
	5. Click "Generate" to show the region map preview. You can keep clicking "Generate" until you are happy with the result.
	6. Once you have a map you like, click "Output Map files".  
	7. Cartographer will produce the following:
		-Many "MapXXX.yaml" files in the YAML folder
		-worldmap.png will be placed in Graphics\Pictures
		-CartographerOutput folder will contain 5 files: encounters.txt, connections.txt, metadata.txt, townmap.txt, 
			trainers.txt, and mapinfos.yaml. There may also be a log file and a "bigWorldMap.png" preview image,
			if either of those were generated.
	8. You will need to open each of the .txt files in the CartographerOutput folder, copy their contents, and paste them
		at the end of the files which have the same names in the PBS folder of your essentials project. (Note: If you
		prefer to manually create your own encounter data by hand, you can ignore encounters.txt)
	9. Do the same thing for mapinfos.yaml, copying the contents from the one in CartographerOutput and paste them at the 
		end of the one in the YAML folder we created earlier in step 3.
	10. Once all the files have been merged, you need to "Pack" all the YAML files back into .rxdata files. To do this,
		click the "Pack Project" button in Cartographer. (it's fine if you've closed & reopened the program, it will
		just pack what is currently in the YAML folder)
	11. You should now see new "MapXXX.rxdata" files in your Data folder - and, you're all set! Open RMXP and check it out.

Generator Options
------------------------------------------------------------------------------------------------------------------------

-You can click "Generate" again to preview a different layout, or click "Output Map Files" to export.
It may take several seconds to generate each region.

-You can also select a number of cities to place, between 3 and 100. Note that if the landmass generated cannot fit the
specified number of cities, it will place the maximum it could fit instead. Lower numbers of cities will not have
8 gyms. The number of cities which can successfully be placed will vary depending on the landmass that is generated, but
generally you will rarely get above 40 or so.

-Optionally, you can enter a unique seed, or leave the "Seed" value blank to use the current system time in milliseconds.

-You can adjust the "loop chance" value, which will affect how often "redundant" routes are generated which connect to areas
that already have at least 1 way to get there. This results in "loops" in the route layout. 

-You can also uncheck the "Place items", "Side stair events", or "Place trainers" options to exclude these things from your 
exported maps.In the case of the "Side stairs", the stairs themselves will still apear, but without events.

-The "Biome Data" tab just lets you view the information that is in CartographerConfig/biomes.txt. Originally I planned
to allow editing this data from this tab but didn't get it working right, so for now it is view-only. You can still edit
the text files directly, though.

-PLEASE NOTE: Currently, the program will use between 1 - 2 GB of RAM while generating maps.





