
# Once PIP is ready, you can start installing packages from PIP:

## pip install package-name
```
pip install package-name
pip install package-name==1.0.0
```

## To search PyPI for a particular package:
```
pip search "query"
```

## To see details about an installed package:
```
pip show package-name
```

## To list all installed packages:
```
pip list
```

## To list all outdated packages:
```
pip list --outdated
```

## To upgrade an outdated package:
- Note that older versions of a package are automatically removed by PIP when upgrading to a newer version of that package.
```
pip install package-name --upgrade
```

## To completely reinstall a package:
```
pip install package-name --upgrade --force-reinstall
```

## To completely get rid of a package:
```
pip uninstall package-name
```