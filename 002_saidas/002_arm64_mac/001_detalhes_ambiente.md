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
      ['3.10.5 | packaged by conda-forge | (main, Jun 14 2022, 07:07:06) [Clang 13.0.1 ]']),
     ('dist', 'N/A'),
     ('linux_distribution', 'N/A'),
     ('system', 'Darwin'),
     ('machine', 'arm64'),
     ('platform', 'macOS-12.4-arm64-arm-64bit'),
     ('uname',
      uname_result(system='Darwin', node='RGOs-MacBook-Pro.local', release='21.5.0', version='Darwin Kernel Version 21.5.0: Tue Apr 26 21:08:37 PDT 2022; root:xnu-8020.121.3~4/RELEASE_ARM64_T6000', machine='arm64')),
     ('version',
      'Darwin Kernel Version 21.5.0: Tue Apr 26 21:08:37 PDT 2022; root:xnu-8020.121.3~4/RELEASE_ARM64_T6000'),
     ('mac_ver', ('12.4', ('', '', ''), 'arm64'))]



### 2.2. Mostra versões das ferramentas CLI


```python
RogerioDetalhesAmbiente.show_versions()
```




    [('python_sys_executable_version', ['Python 3.10.5']),
     ('pip_version',
      ['pip 22.1.2 from /opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente/lib/python3.10/site-packages/pip (python 3.10)']),
     ('conda_version', ['conda 4.12.0']),
     ('mamba_version', ['mamba 0.22.1', 'conda 4.12.0']),
     ('node_version', ['zsh:1: command not found: node']),
     ('npm_version', ['zsh:1: command not found: npm']),
     ('jlpm_version',
      ['Traceback (most recent call last):',
       '  File "/opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente/bin/jlpm", line 10, in <module>',
       '    sys.exit(main())',
       '  File "/opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente/lib/python3.10/site-packages/jupyterlab/jlpmapp.py", line 44, in main',
       '    execvp("node", ["node", YARN_PATH] + argv)',
       '  File "/opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente/lib/python3.10/site-packages/jupyterlab/jlpmapp.py", line 25, in execvp',
       '    cmd = which(cmd)',
       '  File "/opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente/lib/python3.10/site-packages/jupyterlab_server/process.py", line 57, in which',
       '    raise ValueError(msg)',
       'ValueError: Please install Node.js and npm before continuing installation. You may be able to install Node.js from your package manager, from conda, or directly from the Node.js website (https://nodejs.org).'])]



### 2.3. Mostra os ambientes anaconda (conda/mamba) disponíveis


```python
RogerioDetalhesAmbiente.show_anaconda_env_list()
```




    ['# conda environments:',
     '#',
     'base                     /opt/homebrew/Caskroom/mambaforge/base',
     'python-detalhes-ambiente  *  /opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente',
     '']



### 2.4. Mostra os pacotes instalados no ambiente anaconda (conda/mamba)


```python
RogerioDetalhesAmbiente.show_anaconda_pkg_list()
```




    ['# packages in environment at /opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente:',
     '#',
     '# Name                    Version                   Build  Channel',
     'anyio                     3.6.1           py310hbe9552e_0    conda-forge',
     'appnope                   0.1.3              pyhd8ed1ab_0    conda-forge',
     'argon2-cffi               21.3.0             pyhd8ed1ab_0    conda-forge',
     'argon2-cffi-bindings      21.2.0          py310hf8d0d8f_2    conda-forge',
     'asttokens                 2.0.5              pyhd8ed1ab_0    conda-forge',
     'attrs                     21.4.0             pyhd8ed1ab_0    conda-forge',
     'babel                     2.10.3             pyhd8ed1ab_0    conda-forge',
     'backcall                  0.2.0              pyh9f0ad1d_0    conda-forge',
     'backports                 1.0                        py_2    conda-forge',
     'backports.functools_lru_cache 1.6.4              pyhd8ed1ab_0    conda-forge',
     'beautifulsoup4            4.11.1             pyha770c72_0    conda-forge',
     'bleach                    5.0.1              pyhd8ed1ab_0    conda-forge',
     'brotlipy                  0.7.0           py310hf8d0d8f_1004    conda-forge',
     'bzip2                     1.0.8                h3422bc3_4    conda-forge',
     'ca-certificates           2022.6.15            h4653dfc_0    conda-forge',
     'certifi                   2022.6.15       py310hbe9552e_0    conda-forge',
     'cffi                      1.15.1          py310he00a5c5_0    conda-forge',
     'charset-normalizer        2.1.0              pyhd8ed1ab_0    conda-forge',
     'cryptography              37.0.4          py310h94bb23d_0    conda-forge',
     'debugpy                   1.6.0           py310h1105856_0    conda-forge',
     'decorator                 5.1.1              pyhd8ed1ab_0    conda-forge',
     'defusedxml                0.7.1              pyhd8ed1ab_0    conda-forge',
     'entrypoints               0.4                pyhd8ed1ab_0    conda-forge',
     'executing                 0.8.3              pyhd8ed1ab_0    conda-forge',
     'flit-core                 3.7.1              pyhd8ed1ab_0    conda-forge',
     'idna                      3.3                pyhd8ed1ab_0    conda-forge',
     'importlib-metadata        4.11.4          py310hbe9552e_0    conda-forge',
     'importlib_metadata        4.11.4               hd8ed1ab_0    conda-forge',
     'importlib_resources       5.8.0              pyhd8ed1ab_0    conda-forge',
     'ipykernel                 6.15.1             pyh736e0ef_0    conda-forge',
     'ipython                   8.4.0           py310hbe9552e_0    conda-forge',
     'ipython_genutils          0.2.0                      py_1    conda-forge',
     'jedi                      0.18.1          py310hbe9552e_1    conda-forge',
     'jinja2                    3.1.2              pyhd8ed1ab_1    conda-forge',
     'json5                     0.9.5              pyh9f0ad1d_0    conda-forge',
     'jsonschema                4.7.2              pyhd8ed1ab_0    conda-forge',
     'jupyter_client            7.3.4              pyhd8ed1ab_0    conda-forge',
     'jupyter_core              4.10.0          py310hbe9552e_0    conda-forge',
     'jupyter_server            1.16.0             pyhd8ed1ab_0    conda-forge',
     'jupyterlab                3.4.3              pyhd8ed1ab_0    conda-forge',
     'jupyterlab_pygments       0.2.2              pyhd8ed1ab_0    conda-forge',
     'jupyterlab_server         2.15.0             pyhd8ed1ab_0    conda-forge',
     'libcxx                    14.0.6               h04bba0f_0    conda-forge',
     'libffi                    3.4.2                h3422bc3_5    conda-forge',
     'libsodium                 1.0.18               h27ca646_1    conda-forge',
     'libzlib                   1.2.12               ha287fd2_1    conda-forge',
     'markupsafe                2.1.1           py310hf8d0d8f_1    conda-forge',
     'matplotlib-inline         0.1.3              pyhd8ed1ab_0    conda-forge',
     'mistune                   0.8.4           py310he2143c4_1005    conda-forge',
     'nbclassic                 0.3.7              pyhd8ed1ab_0    conda-forge',
     'nbclient                  0.5.13             pyhd8ed1ab_0    conda-forge',
     'nbconvert                 6.4.5           py310hbe9552e_0    conda-forge',
     'nbformat                  5.4.0              pyhd8ed1ab_0    conda-forge',
     'ncurses                   6.3                  h07bb92c_1    conda-forge',
     'nest-asyncio              1.5.5              pyhd8ed1ab_0    conda-forge',
     'notebook                  6.4.12             pyha770c72_0    conda-forge',
     'notebook-shim             0.1.0              pyhd8ed1ab_0    conda-forge',
     'openssl                   1.1.1q               ha287fd2_0    conda-forge',
     'packaging                 21.3               pyhd8ed1ab_0    conda-forge',
     'pandocfilters             1.5.0              pyhd8ed1ab_0    conda-forge',
     'parso                     0.8.3              pyhd8ed1ab_0    conda-forge',
     'pexpect                   4.8.0              pyh9f0ad1d_2    conda-forge',
     'pickleshare               0.7.5                   py_1003    conda-forge',
     'pip                       22.1.2             pyhd8ed1ab_0    conda-forge',
     'prometheus_client         0.14.1             pyhd8ed1ab_0    conda-forge',
     'prompt-toolkit            3.0.30             pyha770c72_0    conda-forge',
     'psutil                    5.9.1           py310h02f21da_0    conda-forge',
     'ptyprocess                0.7.0              pyhd3deb0d_0    conda-forge',
     'pure_eval                 0.2.2              pyhd8ed1ab_0    conda-forge',
     'pycparser                 2.21               pyhd8ed1ab_0    conda-forge',
     'pygments                  2.12.0             pyhd8ed1ab_0    conda-forge',
     'pyopenssl                 22.0.0             pyhd8ed1ab_0    conda-forge',
     'pyparsing                 3.0.9              pyhd8ed1ab_0    conda-forge',
     'pyrsistent                0.18.1          py310hf8d0d8f_1    conda-forge',
     'pysocks                   1.7.1           py310hbe9552e_5    conda-forge',
     'python                    3.10.5          h71ab1a4_0_cpython    conda-forge',
     'python-dateutil           2.8.2              pyhd8ed1ab_0    conda-forge',
     'python-fastjsonschema     2.15.3             pyhd8ed1ab_0    conda-forge',
     'python_abi                3.10                    2_cp310    conda-forge',
     'pytz                      2022.1             pyhd8ed1ab_0    conda-forge',
     'pyzmq                     23.2.0          py310hede2015_0    conda-forge',
     'readline                  8.1.2                h46ed386_0    conda-forge',
     'requests                  2.28.1             pyhd8ed1ab_0    conda-forge',
     'send2trash                1.8.0              pyhd8ed1ab_0    conda-forge',
     'setuptools                63.1.0          py310hbe9552e_0    conda-forge',
     'six                       1.16.0             pyh6c4a22f_0    conda-forge',
     'sniffio                   1.2.0           py310hbe9552e_3    conda-forge',
     'soupsieve                 2.3.1              pyhd8ed1ab_0    conda-forge',
     'sqlite                    3.39.0               h40dfcc0_0    conda-forge',
     'stack_data                0.3.0              pyhd8ed1ab_0    conda-forge',
     'terminado                 0.15.0          py310hbe9552e_0    conda-forge',
     'testpath                  0.6.0              pyhd8ed1ab_0    conda-forge',
     'tk                        8.6.12               he1e0b03_0    conda-forge',
     'tornado                   6.2             py310h02f21da_0    conda-forge',
     'traitlets                 5.3.0              pyhd8ed1ab_0    conda-forge',
     'tzdata                    2022a                h191b570_0    conda-forge',
     'urllib3                   1.26.10            pyhd8ed1ab_0    conda-forge',
     'wcwidth                   0.2.5              pyh9f0ad1d_2    conda-forge',
     'webencodings              0.5.1                      py_1    conda-forge',
     'websocket-client          1.3.3              pyhd8ed1ab_0    conda-forge',
     'wheel                     0.37.1             pyhd8ed1ab_0    conda-forge',
     'xz                        5.2.5                h642e427_1    conda-forge',
     'zeromq                    4.3.4                hbdafb3b_1    conda-forge',
     'zipp                      3.8.0              pyhd8ed1ab_0    conda-forge',
     'zlib                      1.2.12               ha287fd2_1    conda-forge']



### 2.5. Mostra os pacotes instalados no pip


```python
RogerioDetalhesAmbiente.show_pip_freeze()
```




    ['anyio @ file:///Users/runner/miniforge3/conda-bld/anyio_1652463935149/work/dist',
     'appnope @ file:///home/conda/feedstock_root/build_artifacts/appnope_1649077682618/work',
     'argon2-cffi @ file:///home/conda/feedstock_root/build_artifacts/argon2-cffi_1640817743617/work',
     'argon2-cffi-bindings @ file:///Users/runner/miniforge3/conda-bld/argon2-cffi-bindings_1649500378483/work',
     'asttokens @ file:///home/conda/feedstock_root/build_artifacts/asttokens_1618968359944/work',
     'attrs @ file:///home/conda/feedstock_root/build_artifacts/attrs_1640799537051/work',
     'Babel @ file:///home/conda/feedstock_root/build_artifacts/babel_1655419414885/work',
     'backcall @ file:///home/conda/feedstock_root/build_artifacts/backcall_1592338393461/work',
     'backports.functools-lru-cache @ file:///home/conda/feedstock_root/build_artifacts/backports.functools_lru_cache_1618230623929/work',
     'beautifulsoup4 @ file:///home/conda/feedstock_root/build_artifacts/beautifulsoup4_1649463573192/work',
     'bleach @ file:///home/conda/feedstock_root/build_artifacts/bleach_1656355450470/work',
     'brotlipy @ file:///Users/runner/miniforge3/conda-bld/brotlipy_1648854303569/work',
     'certifi==2022.6.15',
     'cffi @ file:///Users/runner/miniforge3/conda-bld/cffi_1656783163977/work',
     'charset-normalizer @ file:///home/conda/feedstock_root/build_artifacts/charset-normalizer_1655906222726/work',
     'cryptography @ file:///Users/runner/miniforge3/conda-bld/cryptography_1657174084384/work',
     'debugpy @ file:///Users/runner/miniforge3/conda-bld/debugpy_1649586398798/work',
     'decorator @ file:///home/conda/feedstock_root/build_artifacts/decorator_1641555617451/work',
     'defusedxml @ file:///home/conda/feedstock_root/build_artifacts/defusedxml_1615232257335/work',
     'entrypoints @ file:///home/conda/feedstock_root/build_artifacts/entrypoints_1643888246732/work',
     'executing @ file:///home/conda/feedstock_root/build_artifacts/executing_1646044401614/work',
     'fastjsonschema @ file:///home/conda/feedstock_root/build_artifacts/python-fastjsonschema_1641751198313/work/dist',
     'flit_core @ file:///home/conda/feedstock_root/build_artifacts/flit-core_1645629044586/work/source/flit_core',
     'idna @ file:///home/conda/feedstock_root/build_artifacts/idna_1642433548627/work',
     'importlib-metadata @ file:///Users/runner/miniforge3/conda-bld/importlib-metadata_1653252869256/work',
     'importlib-resources @ file:///home/conda/feedstock_root/build_artifacts/importlib_resources_1655356668708/work',
     'ipykernel @ file:///Users/runner/miniforge3/conda-bld/ipykernel_1657295113967/work',
     'ipython @ file:///Users/runner/miniforge3/conda-bld/ipython_1653755019776/work',
     'ipython-genutils==0.2.0',
     'jedi @ file:///Users/runner/miniforge3/conda-bld/jedi_1649067433487/work',
     'Jinja2 @ file:///home/conda/feedstock_root/build_artifacts/jinja2_1654302431367/work',
     'json5 @ file:///home/conda/feedstock_root/build_artifacts/json5_1600692310011/work',
     'jsonschema @ file:///home/conda/feedstock_root/build_artifacts/jsonschema-meta_1657629641118/work',
     'jupyter-client @ file:///home/conda/feedstock_root/build_artifacts/jupyter_client_1654730843242/work',
     'jupyter-core @ file:///Users/runner/miniforge3/conda-bld/jupyter_core_1652365483853/work',
     'jupyter-server @ file:///home/conda/feedstock_root/build_artifacts/jupyter_server_1648633996660/work',
     'jupyterlab @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_1654621376725/work',
     'jupyterlab-pygments @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_pygments_1649936611996/work',
     'jupyterlab-server @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_server_1657063151834/work',
     'MarkupSafe @ file:///Users/runner/miniforge3/conda-bld/markupsafe_1648737588665/work',
     'matplotlib-inline @ file:///home/conda/feedstock_root/build_artifacts/matplotlib-inline_1631080358261/work',
     'mistune @ file:///Users/runner/miniforge3/conda-bld/mistune_1635844784701/work',
     'nbclassic @ file:///home/conda/feedstock_root/build_artifacts/nbclassic_1647450696711/work',
     'nbclient @ file:///home/conda/feedstock_root/build_artifacts/nbclient_1646999386773/work',
     'nbconvert @ file:///Users/runner/miniforge3/conda-bld/nbconvert_1648465447893/work',
     'nbformat @ file:///home/conda/feedstock_root/build_artifacts/nbformat_1651607001005/work',
     'nest-asyncio @ file:///home/conda/feedstock_root/build_artifacts/nest-asyncio_1648959695634/work',
     'notebook @ file:///home/conda/feedstock_root/build_artifacts/notebook_1654636967533/work',
     'notebook-shim @ file:///home/conda/feedstock_root/build_artifacts/notebook-shim_1646330736330/work',
     'packaging @ file:///home/conda/feedstock_root/build_artifacts/packaging_1637239678211/work',
     'pandocfilters @ file:///home/conda/feedstock_root/build_artifacts/pandocfilters_1631603243851/work',
     'parso @ file:///home/conda/feedstock_root/build_artifacts/parso_1638334955874/work',
     'pexpect @ file:///home/conda/feedstock_root/build_artifacts/pexpect_1602535608087/work',
     'pickleshare @ file:///home/conda/feedstock_root/build_artifacts/pickleshare_1602536217715/work',
     'prometheus-client @ file:///home/conda/feedstock_root/build_artifacts/prometheus_client_1649447152425/work',
     'prompt-toolkit @ file:///home/conda/feedstock_root/build_artifacts/prompt-toolkit_1656332401605/work',
     'psutil @ file:///Users/runner/miniforge3/conda-bld/psutil_1653089446457/work',
     'ptyprocess @ file:///home/conda/feedstock_root/build_artifacts/ptyprocess_1609419310487/work/dist/ptyprocess-0.7.0-py2.py3-none-any.whl',
     'pure-eval @ file:///home/conda/feedstock_root/build_artifacts/pure_eval_1642875951954/work',
     'pycparser @ file:///home/conda/feedstock_root/build_artifacts/pycparser_1636257122734/work',
     'Pygments @ file:///home/conda/feedstock_root/build_artifacts/pygments_1650904496387/work',
     'pyOpenSSL @ file:///home/conda/feedstock_root/build_artifacts/pyopenssl_1643496850550/work',
     'pyparsing @ file:///home/conda/feedstock_root/build_artifacts/pyparsing_1652235407899/work',
     'pyrsistent @ file:///Users/runner/miniforge3/conda-bld/pyrsistent_1649013428463/work',
     'PySocks @ file:///Users/runner/miniforge3/conda-bld/pysocks_1648857351433/work',
     'python-dateutil @ file:///home/conda/feedstock_root/build_artifacts/python-dateutil_1626286286081/work',
     'pytz @ file:///home/conda/feedstock_root/build_artifacts/pytz_1647961439546/work',
     'pyzmq @ file:///Users/runner/miniforge3/conda-bld/pyzmq_1656183616117/work',
     'requests @ file:///home/conda/feedstock_root/build_artifacts/requests_1656534056640/work',
     'Send2Trash @ file:///home/conda/feedstock_root/build_artifacts/send2trash_1628511208346/work',
     'six @ file:///home/conda/feedstock_root/build_artifacts/six_1620240208055/work',
     'sniffio @ file:///Users/runner/miniforge3/conda-bld/sniffio_1648819417040/work',
     'soupsieve @ file:///home/conda/feedstock_root/build_artifacts/soupsieve_1638550740809/work',
     'stack-data @ file:///home/conda/feedstock_root/build_artifacts/stack_data_1655315839047/work',
     'terminado @ file:///Users/runner/miniforge3/conda-bld/terminado_1652790932906/work',
     'testpath @ file:///home/conda/feedstock_root/build_artifacts/testpath_1645693042223/work',
     'tornado @ file:///Users/runner/miniforge3/conda-bld/tornado_1656938163103/work',
     'traitlets @ file:///home/conda/feedstock_root/build_artifacts/traitlets_1655411388954/work',
     'urllib3 @ file:///home/conda/feedstock_root/build_artifacts/urllib3_1657224465922/work',
     'wcwidth @ file:///home/conda/feedstock_root/build_artifacts/wcwidth_1600965781394/work',
     'webencodings==0.5.1',
     'websocket-client @ file:///home/conda/feedstock_root/build_artifacts/websocket-client_1655796432389/work',
     'zipp @ file:///home/conda/feedstock_root/build_artifacts/zipp_1649012893348/work']



### 2.6. Mostra as extensões jupyter lab


```python
RogerioDetalhesAmbiente.show_jupyter_lab_ext_list()
```




    ['JupyterLab v3.4.3',
     '/opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente/share/jupyter/labextensions',
     '        jupyterlab_pygments v0.2.2 \x1b[32menabled\x1b[0m \x1b[32mOK\x1b[0m (python, jupyterlab_pygments)',
     '']



### 2.7. Mostra as extensões jupyter server


```python
RogerioDetalhesAmbiente.show_jupyter_server_ext_list()
```




    ['    - Validating...',
     '      jupyterlab 3.4.3 \x1b[32mOK\x1b[0m',
     'config dir: /opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente/etc/jupyter',
     '    jupyterlab \x1b[32m enabled \x1b[0m']



### 2.8. Caminho do nosso script no sistema de arquivos


```python
RogerioDetalhesAmbiente.show_current_directory_path()
```




    '/Users/rogeriopradoj/contribs/python-detalhes-ambiente/001_notebooks'



### 2.9. Caminho do diretório pai


```python
RogerioDetalhesAmbiente.show_parent_directory_path()
```




    '/Users/rogeriopradoj/contribs/python-detalhes-ambiente'



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
     '        mamba (0.22.1) supported by @QuantStack',
     '',
     '        GitHub:  https://github.com/mamba-org/mamba',
     '        Twitter: https://twitter.com/QuantStack',
     '',
     '█████████████████████████████████████████████████████████████',
     '',
     '',
     '     active environment : python-detalhes-ambiente',
     '    active env location : /opt/homebrew/Caskroom/mambaforge/base/envs/python-detalhes-ambiente',
     '            shell level : 2',
     '       user config file : /Users/rogeriopradoj/.condarc',
     ' populated config files : /opt/homebrew/Caskroom/mambaforge/base/.condarc',
     '          conda version : 4.12.0',
     '    conda-build version : not installed',
     '         python version : 3.9.13.final.0',
     '       virtual packages : __osx=12.4=0',
     '                          __unix=0=0',
     '                          __archspec=1=arm64',
     '       base environment : /opt/homebrew/Caskroom/mambaforge/base  (writable)',
     '      conda av data dir : /opt/homebrew/Caskroom/mambaforge/base/etc/conda',
     '  conda av metadata url : None',
     '           channel URLs : https://conda.anaconda.org/conda-forge/osx-arm64',
     '                          https://conda.anaconda.org/conda-forge/noarch',
     '          package cache : /opt/homebrew/Caskroom/mambaforge/base/pkgs',
     '                          /Users/rogeriopradoj/.conda/pkgs',
     '       envs directories : /opt/homebrew/Caskroom/mambaforge/base/envs',
     '                          /Users/rogeriopradoj/.conda/envs',
     '               platform : osx-arm64',
     '             user-agent : conda/4.12.0 requests/2.27.1 CPython/3.9.13 Darwin/21.5.0 OSX/12.4',
     '                UID:GID : 502:20',
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
     'channel_priority: flexible',
     'channels:',
     '  - conda-forge',
     'client_ssl_cert: None',
     'client_ssl_cert_key: None',
     'clobber: False',
     'conda_build: {}',
     'create_default_packages: []',
     'croot: /opt/homebrew/Caskroom/mambaforge/base/conda-bld',
     'custom_channels:',
     '  pkgs/main: https://repo.anaconda.com',
     '  pkgs/r: https://repo.anaconda.com',
     '  pkgs/pro: https://repo.anaconda.com',
     'custom_multichannels:',
     '  defaults: ',
     '    - https://repo.anaconda.com/pkgs/main',
     '    - https://repo.anaconda.com/pkgs/r',
     '  local: ',
     'debug: False',
     'default_channels:',
     '  - https://repo.anaconda.com/pkgs/main',
     '  - https://repo.anaconda.com/pkgs/r',
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
     '  - /opt/homebrew/Caskroom/mambaforge/base/envs',
     '  - /Users/rogeriopradoj/.conda/envs',
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
     '  - /opt/homebrew/Caskroom/mambaforge/base/pkgs',
     '  - /Users/rogeriopradoj/.conda/pkgs',
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
     'root_prefix: /opt/homebrew/Caskroom/mambaforge/base',
     'safety_checks: warn',
     'sat_solver: pycosat',
     'separate_format_cache: False',
     'shortcuts: True',
     'show_channel_urls: None',
     'signing_metadata_url_base: None',
     'solver_ignore_timestamps: False',
     'ssl_verify: True',
     'subdir: osx-arm64',
     'subdirs:',
     '  - osx-arm64',
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
