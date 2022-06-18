# 000_detalhes_ambiente.ipynb

<https://github.com/rogeriopradoj/python-detalhes-ambiente>

Notebook que busca detalhar todos os detalhes do ambiente do seu ambiente python / anaconda / jupyter.

Baseado no script disponível <https://stackoverflow.com/a/10091465/1330750>.

## 1. Carrega dependências do script


```python
import os
import platform

import IPython
```

### 1.2. Define classe e métodos


```python
class RogerioDetalhesAmbiente:
    @staticmethod
    def show_platform():
        def linux_distribution():
            try:
                return platform.linux_distribution()
            except:
                return "N/A"
        def dist():
            try:
                return platform.dist()
            except:
                return "N/A"

        results = {}
        method_output = []
        commands = {
            "Python version": os.sys.version.split("\n"),
            "dist": str(dist()),
            "linux_distribution": linux_distribution(),
            "system": platform.system(),
            "machine": platform.machine(),
            "platform": platform.platform(),
            "uname": platform.uname(),
            "version": platform.version(),
            "mac_ver": platform.mac_ver(),
        }

        for tool, tool_command in commands.items():
            tool_result = tool_command
            results[tool] = tool_result

        for tool, tool_result in results.items():
            method_output.append((tool, tool_result))

        return method_output

    @staticmethod
    def show_versions():
        results = {}
        method_output = []
        commands = {
            "python_sys_executable_version": f"{os.sys.executable} --version",
            "pip_version": f"{os.sys.executable} -m pip --version",
            "conda_version": "conda --version",
            "mamba_version": "mamba --version",
            "node_version": "node --version",
            "npm_version": "npm --version",
            "jlpm_version": "jlpm --version",
        }

        for tool, tool_command in commands.items():
            tool_result = !{tool_command}
            if not RogerioDetalhesAmbiente.command_exists(tool_result):
                tool_result = "N/A"
            results[tool] = tool_result

        for tool, tool_result in results.items():
            method_output.append((tool, tool_result))

        return method_output

    @staticmethod
    def show_anaconda_env_list():
        method_output = !mamba env list

        if ( RogerioDetalhesAmbiente.command_exists(method_output) ):
            return method_output

        method_output = !conda env list

        if ( RogerioDetalhesAmbiente.command_exists(method_output) ):
            return "N/A"

        return method_output

    @staticmethod
    def show_anaconda_pkg_list():
        method_output = !mamba list

        if ( RogerioDetalhesAmbiente.command_exists(method_output) ):
            return method_output

        method_output = !conda list

        if ( RogerioDetalhesAmbiente.command_exists(method_output) ):
            return "N/A"

        return method_output

    @staticmethod
    def show_pip_freeze():
        method_output = !pip freeze

        if not RogerioDetalhesAmbiente.command_exists(method_output):
            return "N/A"

        return method_output

    @staticmethod
    def show_jupyter_lab_ext_list():
        method_output = !jupyter labextension list

        if not RogerioDetalhesAmbiente.command_exists(method_output):
            return "N/A"

        return method_output

    @staticmethod
    def show_jupyter_server_ext_list():
        method_output = !jupyter serverextension list

        if not RogerioDetalhesAmbiente.command_exists(method_output):
            return "N/A"

        return method_output

    @staticmethod
    def show_current_directory_path():
        return os.getcwd()

    @staticmethod
    def show_parent_directory_path():
        return os.path.abspath(os.path.join(os.getcwd(), ".."))

    @staticmethod
    def show_anaconda_info():
        method_output = !mamba info

        if ( RogerioDetalhesAmbiente.command_exists(method_output) ):
            return method_output

        method_output = !conda info

        if ( RogerioDetalhesAmbiente.command_exists(method_output) ):
            return "N/A"

        return method_output

    @staticmethod
    def show_anaconda_config_show():
        method_output = !conda config --show

        if not RogerioDetalhesAmbiente.command_exists(method_output):
            return "N/A"

        return method_output

    def command_exists(cli_output: IPython.utils.text.SList):
        return not ( cli_output.spstr.__contains__('reconhecido como um comando') )
```

## 2. Detalhamentos

### 2.1. Mostra detalhes gerais da plataforma


```python
RogerioDetalhesAmbiente.show_platform()
```




    [('Python version',
      ['3.10.4 | packaged by conda-forge | (main, Mar 24 2022, 17:34:17) [MSC v.1929 64 bit (AMD64)]']),
     ('dist', 'N/A'),
     ('linux_distribution', 'N/A'),
     ('system', 'Windows'),
     ('machine', 'AMD64'),
     ('platform', 'Windows-10-10.0.19041-SP0'),
     ('uname',
      uname_result(system='Windows', node='DF7100NB290', release='10', version='10.0.19041', machine='AMD64')),
     ('version', '10.0.19041'),
     ('mac_ver', ('', ('', '', ''), ''))]



### 2.2. Mostra versões das ferramentas CLI


```python
RogerioDetalhesAmbiente.show_versions()
```




    [('python_sys_executable_version', ['Python 3.10.4']),
     ('pip_version',
      ['pip 22.1.2 from c:\\Users\\c066770\\AppData\\Local\\mambaforge\\envs\\atau000013_adi2109_siapa\\lib\\site-packages\\pip (python 3.10)',
       '']),
     ('conda_version', ['conda 4.13.0']),
     ('mamba_version', ['mamba 0.24.0', 'conda 4.13.0']),
     ('node_version', ['v17.9.0']),
     ('npm_version', ['8.5.5']),
     ('jlpm_version', ['1.21.1'])]



### 2.3. Mostra os ambientes anaconda (conda/mamba) disponíveis


```python
RogerioDetalhesAmbiente.show_anaconda_env_list()
```




    ['# conda environments:',
     '#',
     'OCR_DOSSIE               C:\\Users\\c066770\\AppData\\Local\\conda\\conda\\envs\\OCR_DOSSIE',
     'app-fgts-metricas        C:\\Users\\c066770\\AppData\\Local\\conda\\conda\\envs\\app-fgts-metricas',
     'net_normativos           C:\\Users\\c066770\\AppData\\Local\\conda\\conda\\envs\\net_normativos',
     'ocr_dossie               C:\\Users\\c066770\\AppData\\Local\\conda\\conda\\envs\\ocr_dossie',
     'base                     C:\\Users\\c066770\\AppData\\Local\\mambaforge',
     'atau000013_adi2109_siapa  *  C:\\Users\\c066770\\AppData\\Local\\mambaforge\\envs\\atau000013_adi2109_siapa',
     '']



### 2.4. Mostra os pacotes instalados no ambiente anaconda (conda/mamba)


```python
RogerioDetalhesAmbiente.show_anaconda_pkg_list()
```




    ['# packages in environment at C:\\Users\\c066770\\AppData\\Local\\mambaforge\\envs\\atau000013_adi2109_siapa:',
     '#',
     '# Name                    Version                   Build  Channel',
     'anyio                     3.6.1           py310h5588dad_0    conda-forge',
     'appdirs                   1.4.4              pyh9f0ad1d_0    conda-forge',
     'argon2-cffi               21.3.0             pyhd8ed1ab_0    conda-forge',
     'argon2-cffi-bindings      21.2.0          py310he2412df_2    conda-forge',
     'astroid                   2.11.5          py310h5588dad_0    conda-forge',
     'asttokens                 2.0.5              pyhd8ed1ab_0    conda-forge',
     'async_generator           1.10                       py_0    conda-forge',
     'attrs                     21.4.0             pyhd8ed1ab_0    conda-forge',
     'autopep8                  1.5.7              pyhd8ed1ab_0    conda-forge',
     'babel                     2.10.1             pyhd8ed1ab_0    conda-forge',
     'backcall                  0.2.0              pyh9f0ad1d_0    conda-forge',
     'backports                 1.0                        py_2    conda-forge',
     'backports.functools_lru_cache 1.6.4              pyhd8ed1ab_0    conda-forge',
     'beautifulsoup4            4.11.1             pyha770c72_0    conda-forge',
     'black                     22.3.0             pyhd8ed1ab_0    conda-forge',
     'bleach                    5.0.0              pyhd8ed1ab_0    conda-forge',
     'brotlipy                  0.7.0           py310he2412df_1004    conda-forge',
     'bzip2                     1.0.8                h8ffe710_4    conda-forge',
     'ca-certificates           2022.6.15            h5b45459_0    conda-forge',
     'certifi                   2022.6.15       py310h5588dad_0    conda-forge',
     'cffi                      1.15.0          py310hcbf9ad4_0    conda-forge',
     'charset-normalizer        2.0.12             pyhd8ed1ab_0    conda-forge',
     'click                     8.1.3           py310h5588dad_0    conda-forge',
     'colorama                  0.4.4              pyh9f0ad1d_0    conda-forge',
     'cryptography              37.0.2          py310ha857299_0    conda-forge',
     'dataclasses               0.8                pyhc8e2a94_3    conda-forge',
     'debugpy                   1.6.0           py310h8a704f9_0    conda-forge',
     'decorator                 5.1.1              pyhd8ed1ab_0    conda-forge',
     'defusedxml                0.7.1              pyhd8ed1ab_0    conda-forge',
     'dill                      0.3.5.1            pyhd8ed1ab_0    conda-forge',
     'docstring-to-markdown     0.10               pyhd8ed1ab_0    conda-forge',
     'entrypoints               0.4                pyhd8ed1ab_0    conda-forge',
     'executing                 0.8.3              pyhd8ed1ab_0    conda-forge',
     'flake8                    3.9.2              pyhd8ed1ab_0    conda-forge',
     'flit-core                 3.7.1              pyhd8ed1ab_0    conda-forge',
     'gettext                   0.19.8.1          ha2e2712_1008    conda-forge',
     'gitdb                     4.0.9              pyhd8ed1ab_0    conda-forge',
     'gitpython                 3.1.27             pyhd8ed1ab_0    conda-forge',
     'gst-plugins-base          1.20.2               he07aa86_1    conda-forge',
     'gstreamer                 1.20.2               hdff456e_1    conda-forge',
     'h11                       0.13.0             pyhd8ed1ab_1    conda-forge',
     'icu                       70.1                 h0e60522_0    conda-forge',
     'idna                      3.3                pyhd8ed1ab_0    conda-forge',
     'importlib-metadata        4.11.4          py310h5588dad_0    conda-forge',
     'importlib_metadata        4.11.4               hd8ed1ab_0    conda-forge',
     'importlib_resources       5.7.1              pyhd8ed1ab_1    conda-forge',
     'intel-openmp              2022.1.0          h57928b3_3787    conda-forge',
     'ipykernel                 6.13.1          py310hbbfc1a7_0    conda-forge',
     'ipython                   8.4.0           py310h5588dad_0    conda-forge',
     'ipython_genutils          0.2.0                      py_1    conda-forge',
     'ipywidgets                7.7.0              pyhd8ed1ab_0    conda-forge',
     'isort                     5.10.1             pyhd8ed1ab_0    conda-forge',
     'jedi                      0.18.0          py310h5588dad_3    conda-forge',
     'jedi-language-server      0.34.8             pyhd8ed1ab_0    conda-forge',
     'jinja2                    3.1.2              pyhd8ed1ab_1    conda-forge',
     'joblib                    1.1.0              pyhd8ed1ab_0    conda-forge',
     'jpeg                      9e                   h8ffe710_1    conda-forge',
     'json5                     0.9.5              pyh9f0ad1d_0    conda-forge',
     'jsonschema                4.6.0              pyhd8ed1ab_0    conda-forge',
     'jupyter                   1.0.0           py310h5588dad_7    conda-forge',
     'jupyter-lsp               1.5.1              pyhd8ed1ab_0    conda-forge',
     'jupyter-lsp-python        1.5.1              pyhd8ed1ab_0    conda-forge',
     'jupyter-server-mathjax    0.2.5              pyhc268e32_0    conda-forge',
     'jupyter_client            7.3.4              pyhd8ed1ab_0    conda-forge',
     'jupyter_console           6.4.3              pyhd8ed1ab_0    conda-forge',
     'jupyter_contrib_core      0.3.3                      py_2    conda-forge',
     'jupyter_contrib_nbextensions 0.5.1              pyhd8ed1ab_2    conda-forge',
     'jupyter_core              4.10.0          py310h5588dad_0    conda-forge',
     'jupyter_highlight_selected_word 0.2.0           py310h5588dad_1005    conda-forge',
     'jupyter_latex_envs        1.4.6           pyhd8ed1ab_1002    conda-forge',
     'jupyter_nbextensions_configurator 0.4.1              pyhd8ed1ab_2    conda-forge',
     'jupyter_server            1.17.1             pyhd8ed1ab_0    conda-forge',
     'jupyterlab                3.4.3              pyhd8ed1ab_0    conda-forge',
     'jupyterlab-cell-flash     0.3.4              pyhd8ed1ab_0    conda-forge',
     'jupyterlab-git            0.37.1             pyhd8ed1ab_0    conda-forge',
     'jupyterlab-lsp            3.10.1             pyhd8ed1ab_0    conda-forge',
     'jupyterlab_code_formatter 1.4.11             pyhd8ed1ab_0    conda-forge',
     'jupyterlab_execute_time   2.1.0              pyhd8ed1ab_0    conda-forge',
     'jupyterlab_pygments       0.2.2              pyhd8ed1ab_0    conda-forge',
     'jupyterlab_server         2.14.0             pyhd8ed1ab_0    conda-forge',
     'jupyterlab_widgets        1.1.0              pyhd8ed1ab_0    conda-forge',
     'krb5                      1.19.3               h1176d77_0    conda-forge',
     'lazy-object-proxy         1.7.1           py310he2412df_1    conda-forge',
     'libblas                   3.9.0              15_win64_mkl    conda-forge',
     'libcblas                  3.9.0              15_win64_mkl    conda-forge',
     'libclang                  14.0.5          default_h77d9078_0    conda-forge',
     'libclang13                14.0.5          default_h77d9078_0    conda-forge',
     'libffi                    3.4.2                h8ffe710_5    conda-forge',
     'libglib                   2.70.2               h3be07f2_4    conda-forge',
     'libiconv                  1.16                 he774522_0    conda-forge',
     'liblapack                 3.9.0              15_win64_mkl    conda-forge',
     'libogg                    1.3.4                h8ffe710_1    conda-forge',
     'libpng                    1.6.37               h1d00b33_2    conda-forge',
     'libsodium                 1.0.18               h8d14728_1    conda-forge',
     'libvorbis                 1.3.7                h0e60522_0    conda-forge',
     'libxml2                   2.9.14               hf5bbc77_0    conda-forge',
     'libxslt                   1.1.35               h34f844d_0    conda-forge',
     'libzlib                   1.2.12               h8ffe710_0    conda-forge',
     'lxml                      4.9.0           py310he2412df_0    conda-forge',
     'lz4-c                     1.9.3                h8ffe710_1    conda-forge',
     'mamba_gator               5.1.2              pyhd8ed1ab_0    conda-forge',
     'markupsafe                2.1.1           py310he2412df_1    conda-forge',
     'matplotlib-inline         0.1.3              pyhd8ed1ab_0    conda-forge',
     'mccabe                    0.6.1                      py_1    conda-forge',
     'mistune                   0.8.4           py310he2412df_1005    conda-forge',
     'mkl                       2022.1.0           h6a75c08_874    conda-forge',
     'mypy_extensions           0.4.3           py310h5588dad_5    conda-forge',
     'nbclassic                 0.3.7              pyhd8ed1ab_0    conda-forge',
     'nbclient                  0.6.4              pyhd8ed1ab_1    conda-forge',
     'nbconvert                 6.5.0              pyhd8ed1ab_0    conda-forge',
     'nbconvert-core            6.5.0              pyhd8ed1ab_0    conda-forge',
     'nbconvert-pandoc          6.5.0              pyhd8ed1ab_0    conda-forge',
     'nbconvert-webpdf          6.5.0              pyhd8ed1ab_0    conda-forge',
     'nbdime                    3.1.1              pyhd8ed1ab_0    conda-forge',
     'nbformat                  5.4.0              pyhd8ed1ab_0    conda-forge',
     'nest-asyncio              1.5.5              pyhd8ed1ab_0    conda-forge',
     'nodejs                    17.9.0               h57928b3_0    conda-forge',
     'notebook                  6.4.12             pyha770c72_0    conda-forge',
     'notebook-shim             0.1.0              pyhd8ed1ab_0    conda-forge',
     'numpy                     1.22.4          py310hed7ac4c_0    conda-forge',
     'openssl                   1.1.1o               h8ffe710_0    conda-forge',
     'outcome                   1.1.0              pyhd8ed1ab_0    conda-forge',
     'packaging                 21.3               pyhd8ed1ab_0    conda-forge',
     'pandas                    1.4.2           py310hf5e1058_2    conda-forge',
     'pandoc                    2.18                 h57928b3_0    conda-forge',
     'pandocfilters             1.5.0              pyhd8ed1ab_0    conda-forge',
     'parso                     0.8.3              pyhd8ed1ab_0    conda-forge',
     'pathspec                  0.9.0              pyhd8ed1ab_0    conda-forge',
     'pcre                      8.45                 h0e60522_0    conda-forge',
     'pexpect                   4.8.0              pyh9f0ad1d_2    conda-forge',
     'pickleshare               0.7.5                   py_1003    conda-forge',
     'pip                       22.1.2             pyhd8ed1ab_0    conda-forge',
     'platformdirs              2.5.1              pyhd8ed1ab_0    conda-forge',
     'pluggy                    1.0.0           py310h5588dad_3    conda-forge',
     'prometheus_client         0.14.1             pyhd8ed1ab_0    conda-forge',
     'prompt-toolkit            3.0.29             pyha770c72_0    conda-forge',
     'prompt_toolkit            3.0.29               hd8ed1ab_0    conda-forge',
     'psutil                    5.9.1           py310he2412df_0    conda-forge',
     'ptyprocess                0.7.0              pyhd3deb0d_0    conda-forge',
     'pure_eval                 0.2.2              pyhd8ed1ab_0    conda-forge',
     'pycodestyle               2.7.0              pyhd8ed1ab_0    conda-forge',
     'pycparser                 2.21               pyhd8ed1ab_0    conda-forge',
     'pydantic                  1.8.2           py310he2412df_2    conda-forge',
     'pydocstyle                6.1.1              pyhd8ed1ab_0    conda-forge',
     'pyee                      8.1.0              pyhd8ed1ab_0    conda-forge',
     'pyflakes                  2.3.1              pyhd8ed1ab_0    conda-forge',
     'pygls                     0.11.3             pyhd8ed1ab_0    conda-forge',
     'pygments                  2.12.0             pyhd8ed1ab_0    conda-forge',
     'pylint                    2.14.1             pyhd8ed1ab_0    conda-forge',
     'pyopenssl                 22.0.0             pyhd8ed1ab_0    conda-forge',
     'pyparsing                 3.0.9              pyhd8ed1ab_0    conda-forge',
     'pyppeteer                 1.0.2              pyhd8ed1ab_0    conda-forge',
     'pyqt                      5.15.4          py310hbabf5d4_1    conda-forge',
     'pyqt5-sip                 12.9.0          py310h8a704f9_1    conda-forge',
     'pyrsistent                0.18.1          py310he2412df_1    conda-forge',
     'pysocks                   1.7.1           py310h5588dad_5    conda-forge',
     'python                    3.10.4          h9a09f29_0_cpython    conda-forge',
     'python-dateutil           2.8.2              pyhd8ed1ab_0    conda-forge',
     'python-dotenv             0.20.0             pyhd8ed1ab_0    conda-forge',
     'python-fastjsonschema     2.15.3             pyhd8ed1ab_0    conda-forge',
     'python-lsp-jsonrpc        1.0.0              pyhd8ed1ab_0    conda-forge',
     'python-lsp-server         1.2.1              pyhd8ed1ab_0    conda-forge',
     'python_abi                3.10                    2_cp310    conda-forge',
     'pytz                      2022.1             pyhd8ed1ab_0    conda-forge',
     'pywin32                   303             py310he2412df_0    conda-forge',
     'pywinpty                  2.0.5           py310h00ffb61_1    conda-forge',
     'pyyaml                    6.0             py310he2412df_4    conda-forge',
     'pyzmq                     23.1.0          py310h73ada01_0    conda-forge',
     'qt-main                   5.15.4               h467ea89_2    conda-forge',
     'qtconsole                 5.3.1              pyhd8ed1ab_0    conda-forge',
     'qtconsole-base            5.3.1              pyha770c72_0    conda-forge',
     'qtpy                      2.1.0              pyhd8ed1ab_0    conda-forge',
     'requests                  2.28.0             pyhd8ed1ab_0    conda-forge',
     'rope                      1.1.1              pyhd8ed1ab_0    conda-forge',
     'selenium                  4.2.0              pyhd8ed1ab_0    conda-forge',
     'send2trash                1.8.0              pyhd8ed1ab_0    conda-forge',
     'setuptools                62.3.3          py310h5588dad_0    conda-forge',
     'sip                       6.5.1           py310h8a704f9_2    conda-forge',
     'six                       1.16.0             pyh6c4a22f_0    conda-forge',
     'smmap                     3.0.5              pyh44b312d_0    conda-forge',
     'sniffio                   1.2.0           py310h5588dad_3    conda-forge',
     'snowballstemmer           2.2.0              pyhd8ed1ab_0    conda-forge',
     'sortedcontainers          2.4.0              pyhd8ed1ab_0    conda-forge',
     'soupsieve                 2.3.1              pyhd8ed1ab_0    conda-forge',
     'sqlite                    3.38.5               h8ffe710_0    conda-forge',
     'stack_data                0.2.0              pyhd8ed1ab_0    conda-forge',
     'tbb                       2021.5.0             h2d74725_1    conda-forge',
     'terminado                 0.15.0          py310h5588dad_0    conda-forge',
     'tinycss2                  1.1.1              pyhd8ed1ab_0    conda-forge',
     'tk                        8.6.12               h8ffe710_0    conda-forge',
     'toml                      0.10.2             pyhd8ed1ab_0    conda-forge',
     'tomli                     2.0.1              pyhd8ed1ab_0    conda-forge',
     'tomlkit                   0.11.0             pyha770c72_0    conda-forge',
     'tornado                   6.1             py310he2412df_3    conda-forge',
     'tqdm                      4.64.0             pyhd8ed1ab_0    conda-forge',
     'traitlets                 5.2.2.post1        pyhd8ed1ab_0    conda-forge',
     'trio                      0.21.0          py310h5588dad_0    conda-forge',
     'trio-websocket            0.9.2              pyhd8ed1ab_0    conda-forge',
     'typed-ast                 1.5.4           py310he2412df_0    conda-forge',
     'typeguard                 2.13.0             pyhd8ed1ab_0    conda-forge',
     'typing                    3.10.0.0           pyhd8ed1ab_0    conda-forge',
     'typing-extensions         4.2.0                hd8ed1ab_1    conda-forge',
     'typing_extensions         4.2.0              pyha770c72_1    conda-forge',
     'tzdata                    2022a                h191b570_0    conda-forge',
     'ucrt                      10.0.20348.0         h57928b3_0    conda-forge',
     'ujson                     5.3.0           py310h8a704f9_0    conda-forge',
     'urllib3                   1.26.9             pyhd8ed1ab_0    conda-forge',
     'vc                        14.2                 hb210afc_6    conda-forge',
     'vs2015_runtime            14.29.30037          h902a5da_6    conda-forge',
     'wcwidth                   0.2.5              pyh9f0ad1d_2    conda-forge',
     'webencodings              0.5.1                      py_1    conda-forge',
     'websocket-client          1.3.2              pyhd8ed1ab_0    conda-forge',
     'websockets                10.3            py310he2412df_0    conda-forge',
     'wheel                     0.37.1             pyhd8ed1ab_0    conda-forge',
     'widgetsnbextension        3.6.0           py310h5588dad_0    conda-forge',
     'win_inet_pton             1.1.0           py310h5588dad_4    conda-forge',
     'winpty                    0.4.3                         4    conda-forge',
     'wrapt                     1.14.1          py310he2412df_0    conda-forge',
     'wsproto                   1.1.0           py310h5588dad_1    conda-forge',
     'xlrd                      2.0.1              pyhd8ed1ab_3    conda-forge',
     'xz                        5.2.5                h62dcd97_1    conda-forge',
     'yaml                      0.2.5                h8ffe710_2    conda-forge',
     'yapf                      0.32.0             pyhd8ed1ab_0    conda-forge',
     'zeromq                    4.3.4                h0e60522_1    conda-forge',
     'zipp                      3.8.0              pyhd8ed1ab_0    conda-forge',
     'zlib                      1.2.12               h8ffe710_0    conda-forge',
     'zstd                      1.5.2                h6255e5f_1    conda-forge']



### 2.5. Mostra os pacotes instalados no pip


```python
RogerioDetalhesAmbiente.show_pip_freeze()
```




    ['anyio @ file:///D:/bld/anyio_1652464130670/work/dist',
     'appdirs @ file:///home/conda/feedstock_root/build_artifacts/appdirs_1603108395799/work',
     'argon2-cffi @ file:///home/conda/feedstock_root/build_artifacts/argon2-cffi_1640817743617/work',
     'argon2-cffi-bindings @ file:///D:/bld/argon2-cffi-bindings_1649500527917/work',
     'astroid @ file:///D:/bld/astroid_1652112115410/work',
     'asttokens @ file:///home/conda/feedstock_root/build_artifacts/asttokens_1618968359944/work',
     'async-generator==1.10',
     'attrs @ file:///home/conda/feedstock_root/build_artifacts/attrs_1640799537051/work',
     'autopep8 @ file:///home/conda/feedstock_root/build_artifacts/autopep8_1619771482781/work',
     'Babel @ file:///home/conda/feedstock_root/build_artifacts/babel_1651737115240/work',
     'backcall @ file:///home/conda/feedstock_root/build_artifacts/backcall_1592338393461/work',
     'backports.functools-lru-cache @ file:///home/conda/feedstock_root/build_artifacts/backports.functools_lru_cache_1618230623929/work',
     'beautifulsoup4 @ file:///home/conda/feedstock_root/build_artifacts/beautifulsoup4_1649463573192/work',
     'black @ file:///home/conda/feedstock_root/build_artifacts/black-recipe_1648499330704/work',
     'bleach @ file:///home/conda/feedstock_root/build_artifacts/bleach_1649361991009/work',
     'brotlipy @ file:///D:/bld/brotlipy_1648854347500/work',
     'certifi==2022.6.15',
     'cffi @ file:///D:/bld/cffi_1636046270630/work',
     'charset-normalizer @ file:///home/conda/feedstock_root/build_artifacts/charset-normalizer_1644853463426/work',
     'click @ file:///D:/bld/click_1651215332191/work',
     'colorama @ file:///home/conda/feedstock_root/build_artifacts/colorama_1602866480661/work',
     'cryptography @ file:///D:/bld/cryptography_1652967200171/work',
     'dataclasses @ file:///home/conda/feedstock_root/build_artifacts/dataclasses_1628958434797/work',
     'debugpy @ file:///D:/bld/debugpy_1649586532851/work',
     'decorator @ file:///home/conda/feedstock_root/build_artifacts/decorator_1641555617451/work',
     'defusedxml @ file:///home/conda/feedstock_root/build_artifacts/defusedxml_1615232257335/work',
     'dill @ file:///home/conda/feedstock_root/build_artifacts/dill_1653058582944/work',
     'docstring-to-markdown @ file:///home/conda/feedstock_root/build_artifacts/docstring-to-markdown_1637247638475/work',
     'entrypoints @ file:///home/conda/feedstock_root/build_artifacts/entrypoints_1643888246732/work',
     'executing @ file:///home/conda/feedstock_root/build_artifacts/executing_1646044401614/work',
     'fastjsonschema @ file:///home/conda/feedstock_root/build_artifacts/python-fastjsonschema_1641751198313/work/dist',
     'flake8 @ file:///home/conda/feedstock_root/build_artifacts/flake8_1620668104928/work',
     'flit_core @ file:///home/conda/feedstock_root/build_artifacts/flit-core_1645629044586/work/source/flit_core',
     'gitdb @ file:///home/conda/feedstock_root/build_artifacts/gitdb_1635085722655/work',
     'GitPython @ file:///home/conda/feedstock_root/build_artifacts/gitpython_1645531658201/work',
     'h11 @ file:///home/conda/feedstock_root/build_artifacts/h11_1652727116927/work',
     'idna @ file:///home/conda/feedstock_root/build_artifacts/idna_1642433548627/work',
     'importlib-metadata @ file:///D:/bld/importlib-metadata_1653252994979/work',
     'importlib-resources @ file:///home/conda/feedstock_root/build_artifacts/importlib_resources_1652715758048/work',
     'ipykernel @ file:///D:/bld/ipykernel_1654565052815/work',
     'ipython @ file:///D:/bld/ipython_1653755095589/work',
     'ipython-genutils==0.2.0',
     'ipywidgets @ file:///home/conda/feedstock_root/build_artifacts/ipywidgets_1647456365981/work',
     'isort @ file:///home/conda/feedstock_root/build_artifacts/isort_1636447814597/work',
     'jedi @ file:///D:/bld/jedi_1635824174646/work',
     'jedi-language-server @ file:///home/conda/feedstock_root/build_artifacts/jedi-language-server_1635259916374/work',
     'Jinja2 @ file:///home/conda/feedstock_root/build_artifacts/jinja2_1654302431367/work',
     'joblib @ file:///home/conda/feedstock_root/build_artifacts/joblib_1633637554808/work',
     'json5 @ file:///home/conda/feedstock_root/build_artifacts/json5_1600692310011/work',
     'jsonschema @ file:///home/conda/feedstock_root/build_artifacts/jsonschema-meta_1654138136460/work',
     'jupyter @ file:///D:/bld/jupyter_1637233334138/work',
     'jupyter-client @ file:///home/conda/feedstock_root/build_artifacts/jupyter_client_1654730843242/work',
     'jupyter-console @ file:///home/conda/feedstock_root/build_artifacts/jupyter_console_1646669715337/work',
     'jupyter-contrib-core==0.3.3',
     'jupyter-contrib-nbextensions @ file:///home/conda/feedstock_root/build_artifacts/jupyter_contrib_nbextensions_1614931162960/work',
     'jupyter-core @ file:///D:/bld/jupyter_core_1652365483950/work',
     'jupyter-highlight-selected-word @ file:///D:/bld/jupyter_highlight_selected_word_1638383123828/work',
     'jupyter-latex-envs @ file:///home/conda/feedstock_root/build_artifacts/jupyter_latex_envs_1614852190293/work',
     'jupyter-lsp @ file:///home/conda/feedstock_root/build_artifacts/jupyter-lsp-meta_1639326415622/work/jupyter-lsp',
     'jupyter-nbextensions-configurator @ file:///home/conda/feedstock_root/build_artifacts/jupyter_nbextensions_configurator_1614851341942/work',
     'jupyter-server @ file:///home/conda/feedstock_root/build_artifacts/jupyter_server_1654636144140/work',
     'jupyter-server-mathjax @ file:///home/conda/feedstock_root/build_artifacts/jupyter-server-mathjax_1645541128695/work',
     'jupyterlab @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_1654621376725/work',
     'jupyterlab-cell-flash @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab-cell-flash_1631716394785/work',
     'jupyterlab-code-formatter @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_code_formatter_1651414032440/work',
     'jupyterlab-execute-time @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_execute_time_1633144625372/work',
     'jupyterlab-git @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab-git_1650975607360/work',
     'jupyterlab-lsp @ file:///home/conda/feedstock_root/build_artifacts/jupyter-lsp-meta_1647904782549/work/jupyterlab-lsp',
     'jupyterlab-pygments @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_pygments_1649936611996/work',
     'jupyterlab-server @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_server_1652878309867/work',
     'jupyterlab-widgets @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_widgets_1647446862951/work',
     'lazy-object-proxy @ file:///D:/bld/lazy-object-proxy_1649033326177/work',
     'lxml @ file:///D:/bld/lxml_1654081972402/work',
     'mamba-gator @ file:///home/conda/feedstock_root/build_artifacts/mamba_gator-meta_1630671633780/work',
     'MarkupSafe @ file:///D:/bld/markupsafe_1648737731599/work',
     'matplotlib-inline @ file:///home/conda/feedstock_root/build_artifacts/matplotlib-inline_1631080358261/work',
     'mccabe==0.6.1',
     'mistune @ file:///D:/bld/mistune_1635844812333/work',
     'mypy-extensions @ file:///D:/bld/mypy_extensions_1649013486700/work',
     'nbclassic @ file:///home/conda/feedstock_root/build_artifacts/nbclassic_1647450696711/work',
     'nbclient @ file:///home/conda/feedstock_root/build_artifacts/nbclient_1654071785565/work',
     'nbconvert @ file:///home/conda/feedstock_root/build_artifacts/nbconvert-meta_1649676641343/work',
     'nbdime @ file:///home/conda/feedstock_root/build_artifacts/nbdime_1635269257164/work',
     'nbformat @ file:///home/conda/feedstock_root/build_artifacts/nbformat_1651607001005/work',
     'nest-asyncio @ file:///home/conda/feedstock_root/build_artifacts/nest-asyncio_1648959695634/work',
     'notebook @ file:///home/conda/feedstock_root/build_artifacts/notebook_1654636967533/work',
     'notebook-shim @ file:///home/conda/feedstock_root/build_artifacts/notebook-shim_1646330736330/work',
     'numpy @ file:///D:/bld/numpy_1653325554875/work',
     'outcome @ file:///home/conda/feedstock_root/build_artifacts/outcome_1606397708505/work',
     'packaging @ file:///home/conda/feedstock_root/build_artifacts/packaging_1637239678211/work',
     'pandas @ file:///D:/bld/pandas_1653497263811/work',
     'pandocfilters @ file:///home/conda/feedstock_root/build_artifacts/pandocfilters_1631603243851/work',
     'parso @ file:///home/conda/feedstock_root/build_artifacts/parso_1638334955874/work',
     'pathspec @ file:///home/conda/feedstock_root/build_artifacts/pathspec_1626613672358/work',
     'pexpect @ file:///home/conda/feedstock_root/build_artifacts/pexpect_1602535608087/work',
     'pickleshare @ file:///home/conda/feedstock_root/build_artifacts/pickleshare_1602536217715/work',
     'platformdirs @ file:///home/conda/feedstock_root/build_artifacts/platformdirs_1645298319244/work',
     'pluggy @ file:///D:/bld/pluggy_1648772793723/work',
     'prometheus-client @ file:///home/conda/feedstock_root/build_artifacts/prometheus_client_1649447152425/work',
     'prompt-toolkit @ file:///home/conda/feedstock_root/build_artifacts/prompt-toolkit_1649130487073/work',
     'psutil @ file:///D:/bld/psutil_1653089388778/work',
     'ptyprocess @ file:///home/conda/feedstock_root/build_artifacts/ptyprocess_1609419310487/work/dist/ptyprocess-0.7.0-py2.py3-none-any.whl',
     'pure-eval @ file:///home/conda/feedstock_root/build_artifacts/pure_eval_1642875951954/work',
     'pycodestyle @ file:///home/conda/feedstock_root/build_artifacts/pycodestyle_1615833610040/work',
     'pycparser @ file:///home/conda/feedstock_root/build_artifacts/pycparser_1636257122734/work',
     'pydantic @ file:///D:/bld/pydantic_1636021314642/work',
     'pydocstyle @ file:///home/conda/feedstock_root/build_artifacts/pydocstyle_1621377123289/work',
     'pyee @ file:///home/conda/feedstock_root/build_artifacts/pyee_1644152123334/work',
     'pyflakes @ file:///home/conda/feedstock_root/build_artifacts/pyflakes_1616623675904/work',
     'pygls @ file:///home/conda/feedstock_root/build_artifacts/pygls_1636217117670/work/dist',
     'Pygments @ file:///home/conda/feedstock_root/build_artifacts/pygments_1650904496387/work',
     'pylint @ file:///home/conda/feedstock_root/build_artifacts/pylint_1654597844531/work',
     'pyOpenSSL @ file:///home/conda/feedstock_root/build_artifacts/pyopenssl_1643496850550/work',
     'pyparsing @ file:///home/conda/feedstock_root/build_artifacts/pyparsing_1652235407899/work',
     'pyppeteer @ file:///home/conda/feedstock_root/build_artifacts/pyppeteer_1643233645996/work',
     'PyQt5==5.15.4',
     'PyQt5-sip @ file:///D:/bld/pyqt-split_1654255853002/work/pyqt_sip',
     'pyrsistent @ file:///D:/bld/pyrsistent_1649013512562/work',
     'PySocks @ file:///D:/bld/pysocks_1648857426124/work',
     'python-dateutil @ file:///home/conda/feedstock_root/build_artifacts/python-dateutil_1626286286081/work',
     'python-dotenv @ file:///home/conda/feedstock_root/build_artifacts/python-dotenv_1648162816482/work',
     'python-lsp-jsonrpc @ file:///home/conda/feedstock_root/build_artifacts/python-lsp-jsonrpc_1618530352985/work',
     'python-lsp-server @ file:///home/conda/feedstock_root/build_artifacts/python-lsp-server_1628113199343/work',
     'pytz @ file:///home/conda/feedstock_root/build_artifacts/pytz_1647961439546/work',
     'pywin32==303',
     'pywinpty @ file:///D:/bld/pywinpty_1649088350877/work/target/wheels/pywinpty-2.0.5-cp310-none-win_amd64.whl',
     'PyYAML @ file:///D:/bld/pyyaml_1648757288117/work',
     'pyzmq @ file:///D:/bld/pyzmq_1654181546388/work',
     'qtconsole @ file:///home/conda/feedstock_root/build_artifacts/qtconsole-base_1654465674650/work',
     'QtPy @ file:///home/conda/feedstock_root/build_artifacts/qtpy_1651524593465/work',
     'requests @ file:///home/conda/feedstock_root/build_artifacts/requests_1654796491502/work',
     'rope @ file:///home/conda/feedstock_root/build_artifacts/rope_1653489009999/work',
     'selenium @ file:///home/conda/feedstock_root/build_artifacts/selenium_1654004856587/work/src/py',
     'Send2Trash @ file:///home/conda/feedstock_root/build_artifacts/send2trash_1628511208346/work',
     'sip @ file:///D:/bld/sip_1646101407041/work',
     'six @ file:///home/conda/feedstock_root/build_artifacts/six_1620240208055/work',
     'smmap @ file:///home/conda/feedstock_root/build_artifacts/smmap_1611376390914/work',
     'sniffio @ file:///D:/bld/sniffio_1648819361572/work',
     'snowballstemmer @ file:///home/conda/feedstock_root/build_artifacts/snowballstemmer_1637143057757/work',
     'sortedcontainers @ file:///home/conda/feedstock_root/build_artifacts/sortedcontainers_1621217038088/work',
     'soupsieve @ file:///home/conda/feedstock_root/build_artifacts/soupsieve_1638550740809/work',
     'stack-data @ file:///home/conda/feedstock_root/build_artifacts/stack_data_1644872665635/work',
     'terminado @ file:///D:/bld/terminado_1652790796353/work',
     'tinycss2 @ file:///home/conda/feedstock_root/build_artifacts/tinycss2_1637612658783/work',
     'toml @ file:///home/conda/feedstock_root/build_artifacts/toml_1604308577558/work',
     'tomli @ file:///home/conda/feedstock_root/build_artifacts/tomli_1644342247877/work',
     'tomlkit @ file:///home/conda/feedstock_root/build_artifacts/tomlkit_1653380885187/work',
     'tornado @ file:///D:/bld/tornado_1648827438424/work',
     'tqdm @ file:///home/conda/feedstock_root/build_artifacts/tqdm_1649051611147/work',
     'traitlets @ file:///home/conda/feedstock_root/build_artifacts/traitlets_1654067514780/work',
     'trio @ file:///D:/bld/trio_1654688477302/work',
     'trio-websocket @ file:///home/conda/feedstock_root/build_artifacts/trio-websocket_1641849081899/work/dist',
     'typed-ast @ file:///D:/bld/typed-ast_1653226193858/work',
     'typeguard @ file:///home/conda/feedstock_root/build_artifacts/typeguard_1633937540703/work',
     'typing_extensions @ file:///home/conda/feedstock_root/build_artifacts/typing_extensions_1650370875435/work',
     'ujson @ file:///D:/bld/ujson_1653057514151/work',
     'urllib3 @ file:///home/conda/feedstock_root/build_artifacts/urllib3_1647489083693/work',
     'wcwidth @ file:///home/conda/feedstock_root/build_artifacts/wcwidth_1600965781394/work',
     'webencodings==0.5.1',
     'websocket-client @ file:///home/conda/feedstock_root/build_artifacts/websocket-client_1648562593984/work',
     'websockets @ file:///D:/bld/websockets_1650300549706/work',
     'widgetsnbextension @ file:///D:/bld/widgetsnbextension_1647447176344/work',
     'win-inet-pton @ file:///D:/bld/win_inet_pton_1648771897787/work',
     'wrapt @ file:///D:/bld/wrapt_1651495425905/work',
     'wsproto @ file:///D:/bld/wsproto_1652747973550/work',
     'xlrd @ file:///home/conda/feedstock_root/build_artifacts/xlrd_1610224409810/work',
     'yapf @ file:///home/conda/feedstock_root/build_artifacts/yapf_1641487982943/work',
     'zipp @ file:///home/conda/feedstock_root/build_artifacts/zipp_1649012893348/work']



### 2.6. Mostra as extensões jupyter lab


```python
RogerioDetalhesAmbiente.show_jupyter_lab_ext_list()
```




    ['JupyterLab v3.4.3',
     'C:\\Users\\c066770\\AppData\\Local\\mambaforge\\envs\\atau000013_adi2109_siapa\\share\\jupyter\\labextensions',
     '        jupyterlab-cell-flash v0.3.4 enabled ok (python, jupyterlab-cell-flash)',
     '        jupyterlab-execute-time v2.1.0 enabled ok (python, jupyterlab_execute_time)',
     '        jupyterlab_pygments v0.2.2 enabled ok (python, jupyterlab_pygments)',
     '        nbdime-jupyterlab v2.1.1 enabled ok',
     '        @jupyter-widgets/jupyterlab-manager v3.1.0 enabled ok (python, jupyterlab_widgets)',
     '        @jupyterlab/git v0.37.1 enabled ok (python, jupyterlab-git)',
     '        @krassowski/jupyterlab-lsp v3.10.1 enabled ok (python, jupyterlab-lsp)',
     '        @mamba-org/gator-lab v3.0.2 enabled ok (python, mamba_gator)',
     '        @ryantam626/jupyterlab_code_formatter v1.4.11 enabled ok (python, jupyterlab-code-formatter)',
     '',
     'Other labextensions (built into JupyterLab)',
     '   app dir: C:\\Users\\c066770\\AppData\\Local\\mambaforge\\envs\\atau000013_adi2109_siapa\\share\\jupyter\\lab',
     '        @ryantam626/jupyterlab_sublime v0.4.1 enabled ok',
     '        jupyterlab-topbar v0.6.0 enabled ok',
     '']



### 2.7. Mostra as extensões jupyter server


```python
RogerioDetalhesAmbiente.show_jupyter_server_ext_list()
```




    ['config dir: C:\\Users\\c066770\\.jupyter',
     '    jupyter_nbextensions_configurator enabled ',
     '    - Validating...',
     '      jupyter_nbextensions_configurator 0.4.1 ok',
     'config dir: C:\\Users\\c066770\\AppData\\Local\\mambaforge\\envs\\atau000013_adi2109_siapa\\etc\\jupyter',
     '    jupyter_lsp enabled ',
     '    - Validating...',
     '      jupyter_lsp 1.5.1 ok',
     '    jupyterlab enabled ',
     '    - Validating...',
     '      jupyterlab 3.4.3 ok',
     '    jupyterlab_code_formatter enabled ',
     '    - Validating...',
     '      jupyterlab_code_formatter 1.4.11 ok',
     '    jupyterlab_git enabled ',
     '    - Validating...',
     '      jupyterlab_git 0.37.1 ok',
     '    mamba_gator enabled ',
     '    - Validating...',
     '      mamba_gator 5.1.2 ok',
     '    nbdime enabled ',
     '    - Validating...',
     '      nbdime 3.1.1 ok']



### 2.8. Caminho do nosso script no sistema de arquivos


```python
RogerioDetalhesAmbiente.show_current_directory_path()
```




    'c:\\Users\\c066770\\projetos\\cmndd\\python-detalhes-ambiente\\001_notebooks'



### 2.9. Caminho do diretório pai


```python
RogerioDetalhesAmbiente.show_parent_directory_path()
```




    'c:\\Users\\c066770\\projetos\\cmndd\\python-detalhes-ambiente'



### 2.10. Mostra as informações do ambiente anaconda


```python
RogerioDetalhesAmbiente.show_anaconda_info()
```




    ['',
     '                  __    __    __    __',
     '                 /  \\  /  \\  /  \\  /  \\',
     '                /    \\/    \\/    \\/    \\',
     '███████████████/  /██/  /██/  /██/  /████████████████████████',
     '              /  / \\   / \\   / \\   / \\  \\____',
     '             /  /   \\_/   \\_/   \\_/   \\    o \\__,',
     '            / _/                       \\_____/  `',
     '            |/',
     '        ███╗   ███╗ █████╗ ███╗   ███╗██████╗  █████╗',
     '        ████╗ ████║██╔══██╗████╗ ████║██╔══██╗██╔══██╗',
     '        ██╔████╔██║███████║██╔████╔██║██████╔╝███████║',
     '        ██║╚██╔╝██║██╔══██║██║╚██╔╝██║██╔══██╗██╔══██║',
     '        ██║ ╚═╝ ██║██║  ██║██║ ╚═╝ ██║██████╔╝██║  ██║',
     '        ╚═╝     ╚═╝╚═╝  ╚═╝╚═╝     ╚═╝╚═════╝ ╚═╝  ╚═╝',
     '',
     '        mamba (0.24.0) supported by @QuantStack',
     '',
     '        GitHub:  https://github.com/mamba-org/mamba',
     '        Twitter: https://twitter.com/QuantStack',
     '',
     '█████████████████████████████████████████████████████████████',
     '',
     '',
     '     active environment : atau000013_adi2109_siapa',
     '    active env location : C:\\Users\\c066770\\AppData\\Local\\mambaforge\\envs\\atau000013_adi2109_siapa',
     '            shell level : 1',
     '       user config file : C:\\Users\\c066770\\.condarc',
     ' populated config files : C:\\Users\\c066770\\AppData\\Local\\mambaforge\\.condarc',
     '                          C:\\Users\\c066770\\.condarc',
     '          conda version : 4.13.0',
     '    conda-build version : not installed',
     '         python version : 3.9.13.final.0',
     '       virtual packages : __win=0=0',
     '                          __archspec=1=x86_64',
     '       base environment : C:\\Users\\c066770\\AppData\\Local\\mambaforge  (writable)',
     '      conda av data dir : C:\\Users\\c066770\\AppData\\Local\\mambaforge\\etc\\conda',
     '  conda av metadata url : None',
     '           channel URLs : https://conda.anaconda.org/conda-forge/win-64',
     '                          https://conda.anaconda.org/conda-forge/noarch',
     '                          https://repo.anaconda.com/pkgs/main/win-64',
     '                          https://repo.anaconda.com/pkgs/main/noarch',
     '                          https://repo.anaconda.com/pkgs/r/win-64',
     '                          https://repo.anaconda.com/pkgs/r/noarch',
     '                          https://repo.anaconda.com/pkgs/msys2/win-64',
     '                          https://repo.anaconda.com/pkgs/msys2/noarch',
     '          package cache : C:\\Users\\c066770\\AppData\\Local\\mambaforge\\pkgs',
     '                          C:\\Users\\c066770\\.conda\\pkgs',
     '                          C:\\Users\\c066770\\AppData\\Local\\conda\\conda\\pkgs',
     '       envs directories : C:\\Users\\c066770\\AppData\\Local\\mambaforge\\envs',
     '                          C:\\Users\\c066770\\.conda\\envs',
     '                          C:\\Users\\c066770\\AppData\\Local\\conda\\conda\\envs',
     '               platform : win-64',
     '             user-agent : conda/4.13.0 requests/2.27.1 CPython/3.9.13 Windows/10 Windows/10.0.19041',
     '          administrator : False',
     '             netrc file : None',
     '           offline mode : False',
     '']



### 2.11. Mostra as configurações do ambiente anaconda


```python
RogerioDetalhesAmbiente.show_anaconda_config_show()
```




    ['add_anaconda_token: True',
     'add_pip_as_python_dependency: True',
     'aggressive_update_packages:',
     '  - ca-certificates',
     '  - certifi',
     '  - openssl',
     'allow_conda_downgrades: False',
     'allow_cycles: True',
     'allow_non_channel_urls: False',
     'allow_softlinks: False',
     'always_copy: False',
     'always_softlink: False',
     'always_yes: None',
     'anaconda_upload: None',
     'auto_activate_base: True',
     'auto_stack: 0',
     'auto_update_conda: True',
     'bld_path: ',
     'changeps1: True',
     'channel_alias: https://conda.anaconda.org',
     'channel_priority: strict',
     'channels:',
     '  - conda-forge',
     '  - defaults',
     'client_ssl_cert: None',
     'client_ssl_cert_key: None',
     'clobber: False',
     'conda_build: {}',
     'create_default_packages: []',
     'croot: C:\\Users\\c066770\\AppData\\Local\\mambaforge\\conda-bld',
     'custom_channels:',
     '  pkgs/main: https://repo.anaconda.com',
     '  pkgs/r: https://repo.anaconda.com',
     '  pkgs/msys2: https://repo.anaconda.com',
     '  pkgs/pro: https://repo.anaconda.com',
     'custom_multichannels:',
     '  defaults: ',
     '    - https://repo.anaconda.com/pkgs/main',
     '    - https://repo.anaconda.com/pkgs/r',
     '    - https://repo.anaconda.com/pkgs/msys2',
     '  local: ',
     'debug: False',
     'default_channels:',
     '  - https://repo.anaconda.com/pkgs/main',
     '  - https://repo.anaconda.com/pkgs/r',
     '  - https://repo.anaconda.com/pkgs/msys2',
     'default_python: 3.9',
     'default_threads: None',
     'deps_modifier: not_set',
     'dev: False',
     'disallowed_packages: []',
     'download_only: False',
     'dry_run: False',
     'enable_private_envs: False',
     'env_prompt: ({default_env}) ',
     'envs_dirs:',
     '  - C:\\Users\\c066770\\AppData\\Local\\mambaforge\\envs',
     '  - C:\\Users\\c066770\\.conda\\envs',
     '  - C:\\Users\\c066770\\AppData\\Local\\conda\\conda\\envs',
     'error_upload_url: https://conda.io/conda-post/unexpected-error',
     'execute_threads: 1',
     'experimental_solver: classic',
     'extra_safety_checks: False',
     'force: False',
     'force_32bit: False',
     'force_reinstall: False',
     'force_remove: False',
     'ignore_pinned: False',
     'json: False',
     'local_repodata_ttl: 1',
     'migrated_channel_aliases: []',
     'migrated_custom_channels: {}',
     'non_admin_enabled: True',
     'notify_outdated_conda: True',
     'offline: False',
     'override_channels_enabled: True',
     'path_conflict: clobber',
     'pinned_packages: []',
     'pip_interop_enabled: False',
     'pkgs_dirs:',
     '  - C:\\Users\\c066770\\AppData\\Local\\mambaforge\\pkgs',
     '  - C:\\Users\\c066770\\.conda\\pkgs',
     '  - C:\\Users\\c066770\\AppData\\Local\\conda\\conda\\pkgs',
     'proxy_servers: {}',
     'quiet: False',
     'remote_backoff_factor: 1',
     'remote_connect_timeout_secs: 9.15',
     'remote_max_retries: 3',
     'remote_read_timeout_secs: 60.0',
     'repodata_fns:',
     '  - current_repodata.json',
     '  - repodata.json',
     'repodata_threads: None',
     'report_errors: None',
     'restore_free_channel: False',
     'rollback_enabled: True',
     'root_prefix: C:\\Users\\c066770\\AppData\\Local\\mambaforge',
     'safety_checks: warn',
     'sat_solver: pycosat',
     'separate_format_cache: False',
     'shortcuts: True',
     'show_channel_urls: None',
     'signing_metadata_url_base: None',
     'solver_ignore_timestamps: False',
     'ssl_verify: True',
     'subdir: win-64',
     'subdirs:',
     '  - win-64',
     '  - noarch',
     'target_prefix_override: ',
     'track_features: []',
     'unsatisfiable_hints: True',
     'unsatisfiable_hints_check_depth: 2',
     'update_modifier: update_specs',
     'use_index_cache: False',
     'use_local: False',
     'use_only_tar_bz2: False',
     'verbosity: 0',
     'verify_threads: 1',
     'whitelist_channels: []']




```python

```
