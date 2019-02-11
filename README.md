## How To

### First Run

Create `nf.json` with following content:

```json
{
    "name": "testnf",
    "template": "ps",
    "python": "3.7.2",
    "features": [
        "http[starlette]",
        "jupyter"
    ]
}
```

Then run commands on host machine:

```bash
# create local images
$ make

# prepare .nf directory
$ ./nf generate

$ ./nf build
$ ./nf up
```

This will expose:

localhost:8000 - API
localhost:8888 - Jupiter notebook
localhost:2222 - ssh port for tramp connections

Notebooks will be created in `notebooks` directory

Code will be edited in `app` directory


Edit via emacs/tramp:

```elisp
(find-file "/ssh:root@localhost#2222:/app/testnf.py")
```

### Emacs Setup

Add to your config:

```elisp
(use-package
  anaconda-mode
  :ensure t
  :init
  (add-hook 'python-mode-hook #'anaconda-mode)
  (add-hook 'python-mode-hook #'anaconda-eldoc-mode))

(use-package
  company-anaconda
  :ensure t
  :init
  (add-to-list 'company-backends 'company-anaconda)
  :bind
  (:map anaconda-mode-map
        ("M-TAB" . company-complete)))
```
