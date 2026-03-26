
# MSB GAPSEQ PIPELINE

## Prerequisites 
* mamba
* git
* Snakemake
* Have a ssh key registered in GitLab
* Love for metabolic modelling 

## Starting a new project
DISCLAIMER: You should most likely read the `Integrating it into an existing project` section down below (if you use git to manage your files). The current section will make it quite annoying to integrate this pipeline into an existing git project. And because you are a good person you adhere to Thomas' idea of how to structure a project you want to use git for everything :).


`cd` to your local project folder and run `git clone  git@cau-git.rz.uni-kiel.de:MSB/pipelines/gapseq_pipeline.git` and activate your mamba env containing snakemake.
If you do not already have a ssh key setup for gitlab, please read the three links down below or google `How to setup ssh with gitlab`. 

[Link 1](https://docs.gitlab.com/ee/user/ssh.html#generate-an-ssh-key-pair)

[Link 2](https://docs.gitlab.com/ee/user/ssh.html#configure-ssh-to-point-to-a-different-directory)

[Link 3](https://docs.gitlab.com/ee/user/ssh.html#add-an-ssh-key-to-your-gitlab-account)

There is a video tutorial that can be found here [HERE](https://www.youtube.com/watch?v=5Ck07BJDXTE&ab_channel=CameronMcKenzie). It is for windows but that does not matter.

If you wanna learn more about ssh ask ChatGPT :). 

Lets now assume there exist some folder called `MyMAGs` with files called $mag1.fa$ to $magn.fa$ that contains your pre-build MAGs.
To tell the pipeline to use this folder as input open the `config.yaml` and change the `input_folder` and `mag_ending` to the appropriate values. 

ATTENTION: NO COMPRESSED FILES (i.e. no tar.gz, only raw fasta files) ALLOWED. This seems to be a limitation of prodigal nothing can be done there

### Settings 

As mentioned above the settings for the pipeline can be found in the `config.yaml`.
Here you can specify an `out_folder` where all the **produced files** will end up.
If a **custom medium** should be used, specify a path  medium and set `use_medium` to true to use a custom medium.
If you instead want to use the gapseq-predicted media just set `use_medium` to false, the pipeline will the automatically use the gs-predicted media.
Further check if your mags end in `.fna` or change the ending to the appropriate value

### Subsetting the MAGs
If for some reason you want to build models for a subset of your MAGs specify a path in the `keep_list` variable. If for example you just want to build models for $mag3$ and $mag4$. The keep file looks like this
```
mag3.fa
mag4.fa
``` 
I.e. a `\n` separated file of the mag names you want to build models for.

That's all of the input/output configuration you have to do.

### Executing the pipeline 
`cd` into `gapseq_pipeline/workflow`

To run locally execute
```
snakemake --cores <cores> --use-conda
```

To run it on the cluster just execute
```
snakemake --profile settings/
```

To test the pipeline (takes around 2 hours) run
```
snakemake --cores 2 --use-conda
```

## Integrating it into an existing project
`cd` to your local project folder and create a folder called `submodules` and cd into this directory. There create a directory called `configs` which will be empty for now,
and run `git submodule add  git@cau-git.rz.uni-kiel.de:MSB/pipelines/gapseq_pipeline.git`.
The next step is then .... contact Thomas because this is currently fully implemented but not documented


## Contributors

[Dr. Jan Taubenheim](https://github.com/Porthmeus/) (Rewriting gapseq download, various fixes)

## Contributing 

Please contact [Thomas Dost](https://github.com/unaimend) or [Dr. Jan Taubenheim](https://github.com/Porthmeus/)  OR open a pull request 

