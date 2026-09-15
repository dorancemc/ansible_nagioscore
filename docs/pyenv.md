# Install Ansible with pyenv on macOS

`pyenv` manages multiple Python versions, and `pyenv-virtualenv` keeps one virtual environment per tool.

Full docs: <https://github.com/pyenv/pyenv>.

## 1. Install pyenv

```bash
brew install pyenv pyenv-virtualenv
```

## 2. Set up your shell

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
```

Run `exec zsh` to apply.

## 3. Create the environment and install Ansible

```bash
pyenv install 3.14
pyenv virtualenv 3.14 python_3.14_ansible_13.3
pyenv activate python_3.14_ansible_13.3
pip install --upgrade pip
pip install "ansible==13.3" ansible-lint pyfiglet pyaml jmespath passlib yamllint netaddr kubernetes
pyenv deactivate
```

Install `ansible`, not `ansible-core` — the full package ships the required collections (`ansible.posix`, `community.general`).

## 4. Use it in the project

The repo ships a `.python-version` file, so the environment loads automatically. For another project:

```bash
pyenv local python_3.14_ansible_13.3
```

## 5. Check that it works

```bash
ansible --version
ansible-lint --version
yamllint --version
```

`ansible --version` should point to your pyenv environment.
