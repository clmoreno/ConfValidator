#ConfValidator
ConfValidator is a python3 package to easily parse **INI style configuration files**.

You can create a ConfValidator object and add the expected options that the configuration file have, then validate the configuration file and it will produce a dictionary with the configuration you expect.

##Getting started:

###Installation

```bash
pip install ConfValidator
```
or
```bash
easy_install ConfValidator
```

###Basic Validation

```python
# Expamle

import ConfValidator

# Create the object
my_config  = ConfValidator.ConfValidator('/Path/to/my/configFile.cfg')

# Add simple option to the expected configuration.
my_config.add_option(option='username', required=True)

# Add a selction to the expected configuration.
my_config.add_selection(options=['password','ssk-key'], required=True)

# Validate the configuration
try:
    my_config.validate()
except Exception as e:
    exit(e)

# If no errors parsing and validating the configuration file, get resultant dictionary.
my_config.config

```

###add_option()
This operation allows to add an expected option to the ConfValidator object. 

As an example assume you need the user name in the configuration file, so you can use add_option() as follows.
```python
# Expamle

my_config.option(option='user', required=True)
```

#####Params
```python
:param option: <String> <required> Name of the option.
:param required: <bool> If True the option must be present in the configuration file. Default: False
:param valid_values: <list> If specified, the option must contain some of these values.
:param default_value: <String> If value or option are not present this is the default value. Default: None
```


###add_selection()
Some times is needed to have one of many of options in the configuration file, this operation allows to add a selection of options to the ConfValidator object.

As an example assume you need an authentication method for your app, it can be ssh-key, password or token.
You need only one of them, so you can use add_selection() as follows.
```python
# Expamle

my_config.selection(options=['ssh-key', 'password', 'token'], required=True)
```

#####Params
```python
:param options: <list> <required> A list of valid option in the configuration file, one of this options must be present in the configuration file.
:param required: <bool> If True the option must be present in the configuration file. Default: False
:param valid_values: :param valid_values: <list> If specified the option must contain some of these values.
:param default_value:  <String> If value is not present this is the default value. Default: None
:param default_option:  <String> If option is not present this is the default value. Default: None
```


###valid_values argument
Can limit the value in the configuration to allow only one of the specified values.

```python
# Expamle

# Any other value than user or user2 is not allowed
my_config.option(option='user', required=True, valid_values=['user1', 'user2'])
```


###default_value argument
If the specified option is not present this will be the default value.

```python
# Expamle

# If option is not present the value will be Administrator
my_config.option(option='user', required=True, default_value='Administrator')
```
