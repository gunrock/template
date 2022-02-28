# 👻 Library Template for Essentials

Would like to get started with [gunrock/essentials](https://github.com/gunrock/essentials)? Use this template as an example to get your build set-up! For more information about `gunrock/essentials` please visit the [wiki](https://github.com/gunrock/essentials/wiki).

## Getting Started
- Click "Use this template" button on github to create your own repository.
- Use the following instructions below to build the project.
- Make sure to change `<username>/<repo-name>` to your repository.
```bash
git clone https://github.com/<username>/<repo-name>.git
cd <repo-name>
mkdir build && cd build
cmake .. 
make hello
bin/hello
```

### Code Base Explained
Very simple directory structure, add your source files to `src`. We provide an example of `hello.cu` that uses `gunrock`'s namespace.
```
.
├── CMakeLists.txt ➝ Set this project as a library
├── README.md
├── cmake
│   └── FetchEssentials.cmake ➝ Fetches essentials
├── externals ➝ Empty directory to download projects
└── src
    └── hello.cu ➝ Example executable

3 directories, 4 files
```
