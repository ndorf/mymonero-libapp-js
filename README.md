## General dependencies
The MyMonero libapp build requires you to have installed docker. Docker should be in your system's evironment path.

## Building libapp

1. Clone the repo `git clone https://github.com/mymonero/mymonero-libapp-js.git`
2. `cd mymonero-libapp-js`
3. Run `bin/update_submodules`
4. Download Boost libraries
* `curl -LO https://dl.bintray.com/boostorg/release/1.69.0/source/boost_1_69_0.tar.gz` or `wget https://dl.bintray.com/boostorg/release/1.69.0/source/boost_1_69_0.tar.gz` - For Mac, you can verify the integrity of the archive by running `shasum -a 256 boost_1_69_0.tar.gz`. You should see the following hash: `9a2c2819310839ea373f42d69e733c339b4e9a19deab6bfec448281554aa4dbb`
5. `mkdir -p contrib/boost-sdk`
6. `tar zxf boost_1_69_0.tar.gz -C contrib/boost-sdk --strip-components=1`
7. `rm -rf build && mkdir build`
8. `rm libapp_js/MyMoneroLibAppCpp_*`

### Build boost emscripten
9. `docker run --rm -it -v $(pwd):/app -w /app emscripten/emsdk ./bin/build-boost-emscripten.sh`

### Build MyMonero emscripten
10. `docker run --rm -it -v $(pwd):/app -w /app -e EMSCRIPTEN=/emsdk/upstream/emscripten emscripten/emsdk ./bin/archive-emcpp.sh`
 * If you get '#error Including <emscripten/bind.h> requires building with -std=c++11 or newer!' error, re-run step 10. 
 
 By following these instructions, new WASM and ASM libraries are generated and copied to the libapp_js folder
