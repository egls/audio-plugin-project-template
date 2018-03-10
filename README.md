# audio-plugin-project-template #
[![Build Status](https://travis-ci.org/shaduzlabs/audio-plugin-project-template.svg?branch=master)](https://travis-ci.org/shaduzlabs/audio-plugin-project-template) [![Build status](https://ci.appveyor.com/api/projects/status/i0wh7uibh7m9uem9/branch/master?svg=true)](https://ci.appveyor.com/project/shaduzlabs/audio-plugin-project-template/branch/master)

This project provides configuration files and some cmake utilities to speed-up the development of [JUCE][55017f87]-based audio plugins. What you'll get:
- [Travis CI][f595581b] integration (OS X builds)
- [Appveyor][13860100] integration (Windows builds)
- Automatic deployment of release binaries using GitHub releases
- JUCE and VST3 sdk as submodules
- JUCE/cmake integration
- A simple example (a gain control plugin)

![The plugin UI](support/images/screenshot.png)

## Configure Appveyor ##
- Authorize access for Appveyor to your GitHub profile and add the plugin project
- Create a GitHub access token with a name like "Appveyor token for deployment" and select only `public_repo`
- Encrypt the token using [this form][95921ad4]
- Replace the content of `deploy.auth_token.secure` in `.appveyor.yml` with the encrypted string generated by the form

## Configure Travis CI ##
- Authorize access for Travis CI to your GitHub profile and add the plugin project
- Create a GitHub access token with a name like "Travis CI token for deployment" and select only `public_repo`
- Encrypt the token using the [command line utility][feb7d597]
- Replace the content of `deploy.api_key.secure` in `.travis.yml` with the encrypted string generated by the utility

## Release ##
- The creation of a new release on GitHub will trigger new builds (and automatic deployments, once the builds are succesfully completed) on Appveyor and Travis CI
- As an alternative, you can manually add a tag to the `master` branch: `git tag vX.Y.Z` and then push it `git push --tags`

## Building on OS X ##
- Make sure cmake, git and Xcode are installed (if not, the first two can be installed via [brew][dbaaa0fa], while Xcode can be downloaded from the App Store)
- From the terminal, run:
  - `git clone https://github.com/shaduzlabs/audio-plugin-project-template.git` --recursive
  - `cd audio-plugin-project-template`
  - `mkdir build`
  - `cd build`
  - `cmake -DCMAKE_OSX_ARCHITECTURES="i386;x86_64" -G Xcode ..`
  - `cmake --build . --config Release`
  - Now you should have the following bundles:
    - `build/Release/gain.vst`
    - `build/Release/gain.vst3`
    - `build/Release/gain.component`

## Building on Windows ##
- Make sure cmake, git and Visual Studio 2015 are installed
- From the command prompt, run:
  - `git clone https://github.com/shaduzlabs/audio-plugin-project-template.git` --recursive
  - `cd audio-plugin-project-template`
  - `mkdir build`
  - `cd build`
  - `cmake -G "Visual Studio 14 2015 Win64" ..` to build the 64 bit version or `cmake -G "Visual Studio 14 2015" ..` to build the 32 bit version
  - `cmake --build . --config Release`
  - Now you should have the following bundles:
    - `build/Release/gain.dll`
    - `build/Release/gain-vst3.dll`


  [55017f87]: http://juce.com "The JUCE framework"
  [f595581b]: http://travis-ci.org/ "Travis CI"
  [13860100]: https://www.appveyor.com "Appveyor"
  [95921ad4]: https://ci.appveyor.com/tools/encrypt "Encrypt access token"
  [feb7d597]: http://docs.travis-ci.com/user/encryption-keys "How to encrypt strings for Travis CI"
  [dbaaa0fa]: https://brew.sh "Install brew"
