## Teradata Python package for Advanced Analytics.

teradataml makes available to Python users a collection of analytic functions that reside on Teradata Vantage. This allows users to perform analytics on Teradata Vantage with no SQL coding. In addition, the teradataml library provides functions for scaling data manipulation and transformation, data filtering and sub-setting, and can be used in conjunction with other open-source python libraries.

For community support, please visit the [Teradata Community](https://support.teradata.com/community?id=community_forum&sys_id=14fe131e1bf7f304682ca8233a4bcb1d).

For Teradata customer support, please visit [Teradata Support](https://support.teradata.com/csm).

Copyright 2024, Teradata. All Rights Reserved.

### Table of Contents
* [Release Notes](#release-notes)
* [Installation and Requirements](#installation-and-requirements)
* [Using the Teradata Python Package](#using-the-teradata-python-package)
* [Documentation](#documentation)
* [License](#license)

## Release Notes:
#### teradataml 20.00.00.02

* teradataml will no longer be supported with SQLAlchemy < 2.0.
* teradataml no longer shows the warnings from Vantage by default. 
  * Users should set `display.suppress_vantage_runtime_warnings` to `False` to display warnings.

* ##### New Features/Functionality
  * ##### teradataml: SQLE Engine Analytic Functions
    * New Analytics Database Analytic Functions:
      * `TFIDF()`
      * `Pivoting()`
      * `UnPivoting()`
    * New Unbounded Array Framework(UAF) Functions:
      * `AutoArima()`
      * `DWT()`
      * `DWT2D()`
      * `FilterFactory1d()`  
      * `IDWT()`
      * `IDWT2D()`
      * `IQR()`
      * `Matrix2Image()`
      * `SAX()`
      * `WindowDFFT()`
  * ###### teradataml: Functions
      * `udf()` - Creates a user defined function (UDF) and returns ColumnExpression.
      * `set_session_param()` is added to set the database session parameters. 
      * `unset_session_param()` is added to unset database session parameters.
  
  * ###### teradataml: DataFrame
      * `materialize()` - Persists DataFrame into database for current session.
      * `create_temp_view()` - Creates a temporary view for session on the DataFrame.

  * ###### teradataml DataFrameColumn a.k.a. ColumnExpression
      * _Date Time Functions_
        * `DataFrameColumn.to_timestamp()` - Converts string or integer value to a TIMESTAMP data type or TIMESTAMP WITH TIME ZONE data type.
        * `DataFrameColumn.extract()` - Extracts date component to a numeric value.
        * `DataFrameColumn.to_interval()` - Converts a numeric value or string value into an INTERVAL_DAY_TO_SECOND or INTERVAL_YEAR_TO_MONTH value.
      * _String Functions_
        * `DataFrameColumn.parse_url()` - Extracts a part from a URL.
      * _Arithmetic Functions_
        * `DataFrameColumn.log` - Returns the logarithm value of the column with respect to 'base'.

  * ##### teradataml: AutoML
      * New methods added for `AutoML()`, `AutoRegressor()` and `AutoClassifier()`:
        * `evaluate()` - Performs evaluation on the data using the best model or the model of users choice
          from the leaderboard.
        * `load()`: Loads the saved model from database.
        * `deploy()`: Saves the trained model inside database.
        * `remove_saved_model()`: Removes the saved model in database.
        * `model_hyperparameters()`: Returns the hyperparameter of fitted or loaded models.

* ##### Updates
  * ##### teradataml: AutoML
    * `AutoML()`, `AutoRegressor()`
      * New performance metrics added for task type regression i.e., "MAPE", "MPE", "ME", "EV", "MPD" and "MGD".
    * `AutoML()`, `AutoRegressor()` and `AutoClassifier`
      * New arguments added: `volatile`, `persist`.
      * `predict()` - Data input is now mandatory for generating predictions. Default model 
      evaluation is now removed.
  * `DataFrameColumn.cast()`: Accepts 2 new arguments `format` and `timezone`.
  * `DataFrame.assign()`: Accepts ColumnExpressions returned by `udf()`.

  * ##### teradataml: Options
    * `set_config_params()`
      * Following arguments will be deprecated in the future:
        * `ues_url`
        * `auth_token`

  * ###### Database Utility
      * `list_td_reserved_keywords()` - Accepts a list of strings as argument.

  * ##### Updates to existing UAF Functions:
    * `ACF()` - `round_results` parameter removed as it was used for internal testing.
    * `BreuschGodfrey()` - Added default_value 0.05 for parameter `significance_level`.
    * `GoldfeldQuandt()` - 
      * Removed parameters  `weights` and `formula`.
        Replaced parameter `orig_regr_paramcnt` with `const_term`.
        Changed description for parameter `algorithm`. Please refer document for more details.
      * Note: This will break backward compatibility.
    * `HoltWintersForecaster()` - Default value of parameter `seasonal_periods` removed.
    * `IDFFT2()` - Removed parameter `output_fmt_row_major` as it is used for internal testing.
    * `Resample()` - Added parameter `output_fmt_index_style`.

* ##### Bug Fixes
  * KNN `predict()` function can now predict on test data which does not contain target column.
  * Metrics functions are supported on the Lake system.
  * The following OpensourceML functions from different sklearn modules are fixed.
    * `sklearn.ensemble`:
      * ExtraTreesClassifier - `apply()`
      * ExtraTreesRegressor - `apply()`
      * RandomForestClassifier - `apply()`
      * RandomForestRegressor - `apply()`
    * `sklearn.impute`:
      * SimpleImputer - `transform()`, `fit_transform()`, `inverse_transform()`
      * MissingIndicator - `transform()`, `fit_transform()`
    * `sklearn.kernel_approximations`:
      * Nystroem - `transform()`, `fit_transform()`
      * PolynomialCountSketch - `transform()`, `fit_transform()`
      * RBFSampler - `transform()`, `fit_transform()`
    * `sklearn.neighbours`:
      * KNeighborsTransformer - `transform()`, `fit_transform()`
      * RadiusNeighborsTransformer - `transform()`, `fit_transform()`
    * `sklearn.preprocessing`:
      * KernelCenterer - `transform()`
      * OneHotEncoder - `transform()`, `inverse_transform()`
  * OpensourceML returns teradataml objects for model attributes and functions instead of sklearn
    objects so that the user can perform further operations like `score()`, `predict()` etc on top
    of the returned objects.
  * AutoML `predict()` function now generates correct ROC-AUC value for positive class.
  * `deploy()` method of `Script` and `Apply` classes retries model deployment if there is any 
    intermittent network issues.

#### teradataml 20.00.00.01
* teradataml no longer supports Python versions less than 3.8.

* ##### New Features/Functionality
  * ##### Personal Access Token (PAT) support in teradataml
    * `set_auth_token()` - teradataml now supports authentication via PAT in addition to 
      OAuth 2.0 Device Authorization Grant (formerly known as the Device Flow).
      * It accepts UES URL, Personal AccessToken (PAT) and Private Key file generated from VantageCloud Lake Console 
        and optional argument `username` and `expiration_time` in seconds. 

* ##### Updates
  * ##### teradataml: SQLE Engine Analytic Functions
    * `ANOVA()`
      * New arguments added: `group_name_column`, `group_value_name`, `group_names`, `num_groups` for data containing group values and group names. 
    * `FTest()`
      * New arguments added: `sample_name_column`, `sample_name_value`, `first_sample_name`, `second_sample_name`.
    * `GLM()`
      * Supports stepwise regression and accept new arguments `stepwise_direction`, `max_steps_num` and `initial_stepwise_columns`.
      * New arguments added: `attribute_data`, `parameter_data`, `iteration_mode` and `partition_column`.
    * `GetFutileColumns()`
      * Arguments `category_summary_column` and `threshold_value` are now optional.
    * `KMeans()`
      * New argument added: `initialcentroids_method`.
    * `NonLinearCombineFit()`
        * Argument `result_column` is now optional.
    * `ROC()`
        * Argument `positive_class` is now optional. 
    * `SVMPredict()`
      * New argument added: `model_type`.   
    * `ScaleFit()`
      * New arguments added: `ignoreinvalid_locationscale`, `unused_attributes`, `attribute_name_column`, `attribute_value_column`.
      * Arguments `attribute_name_column`, `attribute_value_column` and `target_attributes` are supported for sparse input.
      * Arguments `attribute_data`, `parameter_data` and `partition_column` are supported for partitioning.
    * `ScaleTransform()`
      * New arguments added: `attribute_name_column` and `attribute_value_column` support for sparse input.
    * `TDGLMPredict()`
      * New arguments added: `family` and `partition_column`.
    * `XGBoost()`
      * New argument `base_score` is added for initial prediction value for all data points.
    * `XGBoostPredict()`
      * New argument `detailed` is added for detailed information of each prediction.
    * `ZTest()`
      * New arguments added: `sample_name_column`, `sample_value_column`,  `first_sample_name` and `second_sample_name`.
  * ##### teradataml: AutoML
    * `AutoML()`, `AutoRegressor()` and `AutoClassifier()`
      * New argument `max_models` is added as an early stopping criterion to limit the maximum number of models to be trained.
  * ##### teradataml: DataFrame functions
    * `DataFrame.agg()` 
      * Accepts ColumnExpressions and list of ColumnExpressions as arguments.
  * ##### teradataml: General Functions
    * Data Transfer Utility
      * `fastload()` - Improved error and warning table handling with below-mentioned new arguments.
        * `err_staging_db`
        * `err_tbl_name`
        * `warn_tbl_name`
        * `err_tbl_1_suffix`
        * `err_tbl_2_suffix`
      * `fastload()` - Change in behaviour of `save_errors` argument.
                       When `save_errors` is set to `True`, error information will be available in two persistent tables `ERR_1` and `ERR_2`.
                       When `save_errors` is set to `False`, error information will be available in single pandas dataframe.
    * Garbage collector location is now configurable. 
      User can set configure.local_storage to a desired location.
      
* ##### Bug Fixes
  * UAF functions now work if the database name has special characters.
  * OpensourceML can now read and process NULL/nan values.
  * Boolean values output will now be returned as VARBYTE column with 0 or 1 values in OpensourceML.
  * Fixed bug for `Apply`'s `deploy()`.
  * Issue with volatile table creation is fixed where it is created in the right database, i.e., user's spool space, regardless of the temp database specified.
  * `ColumnTransformer` function now processes its arguments in the order they are passed.

#### teradataml 20.00.00.00
* ##### New Features/Functionality
    * ###### teradataml OpenML: Run Opensource packages through Teradata Vantage
      `OpenML` dynamically exposes opensource packages through Teradata Vantage. `OpenML` provides an
      interface object through which exposed classes and functions of opensource packages can be accessed
      with the same syntax and arguments. 
      The following functionality is added in the current release:
      * `td_sklearn` - Interface object to run scikit-learn functions and classes through Teradata Vantage.
      Example usage below:
        ```
        from teradataml import td_sklearn, DataFrame

        df_train = DataFrame("multi_model_classification")

        feature_columns = ["col1", "col2", "col3", "col4"]
        label_columns = ["label"]
        part_columns = ["partition_column_1", "partition_column_2"]

        linear_svc = td_sklearn.LinearSVC()
        ```
      * `OpenML` is supported in both Teradata Vantage Enterprise and Teradata Vantage Lake.
      * Argument Support:
        * `Use of X and y arguments` - Scikit-learn users are familiar with using `X` and `y` as argument names
        which take data as pandas DataFrames, numpy arrays or lists etc. However, in OpenML, we pass 
        teradataml DataFrames for arguments `X` and `y`.
          ```
          df_x = df_train.select(feature_columns)
          df_y = df_train.select(label_columns)

          linear_svc = linear_svc.fit(X=df_x, y=df_y)
          ```
        * `Additional support for data, feature_columns, label_columns and group_columns arguments` -
        Apart from traditional arguments, OpenML supports additional arguments - `data`,
        `feature_columns`, `label_columns` and `group_columns`. These are used as alternatives to `X`, `y`
        and `groups`.
          ```
          linear_svc = linear_svc.fit(data=df_train, feature_columns=feature_columns, label_colums=label_columns)
          ```
      * `Support for classification and regression metrics` - Metrics functions for classification and
      regression in `sklearn.metrics` module are supported. Other metrics functions' support will be added
      in future releases.
      * `Distributed Modeling and partition_columns argument support` - Existing scikit-learn supports 
      only single model generation. However, OpenML supports both single model use case and distributed
      (multi) model use case. For this, user has to additionally pass `partition_columns` argument to 
      existing `fit()`, `predict()` or any other function to be run. This will generate multiple models
      for multiple partitions, using the data in corresponding partition.
        ```
        df_x_1 = df_train.select(feature_columns + part_columns)
        linear_svc = linear_svc.fit(X=df_x_1, y=df_y, partition_columns=part_columns)      
        ```
      * `Support for load and deploy models` - OpenML provides additional support for saving (deploying) the
      trained models. These models can be loaded later to perform operations like prediction, score etc. The
      following functions are provided by OpenML:
        * `<obj>.deploy()` - Used to deploy/save the model created and/or trained by OpenML.
        * `td_sklearn.deploy()` - Used to deploy/save the model created and/or trained outside teradataml.
        * `td_sklearn.load()` - Used to load the saved models.
      
      <br>Refer Teradata Python Package User Guide for more details of this feature, arguments, usage, examples and supportability in both VantageCloud Enterprise and VantageCloud Lake.

    * ###### teradataml: AutoML - Automated end to end Machine Learning flow.
      AutoML is an approach to automate the process of building, training, and validating machine learning models. 
      It involves automation of various aspects of the machine learning workflow, such as feature exploration, 
      feature engineering, data preparation, model training and evaluation for given dataset.
      teradataml AutoML feature offers best model identification, model leaderboard generation, parallel execution, 
      early stopping feature, model evaluation, model prediction, live logging, customization on default process.
      * `AutoML`
        AutoML is a generic algorithm that supports all three tasks, i.e. 'Regression',
        'Binary Classification' and 'Multiclass Classification'. 
        * Methods of AutoML
          * `__init__()` - Instantiate an object of AutoML with given parameters.
          * `fit()` - Perform fit on specified data and target column.
          * `leaderboard()` - Get the leaderboard for the AutoML. Presents diverse models, feature 
          selection method, and performance metrics.
          * `leader()` - Show best performing model and its details such as feature 
          selection method, and performance metrics.
          * `predict()` - Perform prediction on the data using the best model or the model of users 
          choice from the leaderboard.
          * `generate_custom_config()` - Generate custom config JSON file required for customized 
          run of AutoML.
      * `AutoRegressor`
        AutoRegressor is a special purpose AutoML feature to run regression specific tasks. 
        * Methods of AutoRegressor
          * `__init__()` - Instantiate an object of AutoRegressor with given parameters.
          * `fit()` - Perform fit on specified data and target column.
          * `leaderboard()` - Get the leaderboard for the AutoRegressor. Presents diverse models, feature 
          selection method, and performance metrics.
          * `leader()` - Show best performing model and its details such as feature 
          selection method, and performance metrics.
          * `predict()` - Perform prediction on the data using the best model or the model of users 
          choice from the leaderboard.
          * `generate_custom_config()` - Generate custom config JSON file required for customized 
          run of AutoRegressor.
      * `AutoClassifier`
        AutoClassifier is a special purpose AutoML feature to run classification specific tasks.
        * Methods of AutoClassifier
          * `__init__()` - Instantiate an object of AutoClassifier with given parameters.
          * `fit()` - Perform fit on specified data and target column.
          * `leaderboard()` - Get the leaderboard for the AutoClassifier. Presents diverse models, feature 
          selection method, and performance metrics.
          * `leader()` - Show best performing model and its details such as feature 
          selection method, and performance metrics.
          * `predict()` - Perform prediction on the data using the best model or the model of users 
          choice from the leaderboard.
          * `generate_custom_config()` - Generate custom config JSON file required for customized 
          run of AutoClassifier.

    * ###### teradataml: DataFrame
      * `fillna` - Replace the null values in a column with the value specified. 
      * Data Manipulation
          * `cube()`- Analyzes data by grouping it into multiple dimensions.
          * `rollup()` - Analyzes a set of data across a single dimension with more than one level of detail.
          * `replace()` - Replaces the values for columns.

    * ###### teradataml: Script and Apply
      * `deploy()` - Function deploys the model, generated after `execute_script()`, in database or user
            environment in lake. The function is available in both Script and Apply.

    * ###### teradataml: DataFrameColumn
      * `fillna` - Replaces every occurrence of null value in column with the value specified.
    
* ###### teradataml DataFrameColumn a.k.a. ColumnExpression
    * _Date Time Functions_
      * `DataFrameColumn.week_start()` - Returns the first date or timestamp of the week that begins immediately before the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.week_begin()` - It is an alias for `DataFrameColumn.week_start()` function.
      * `DataFrameColumn.week_end()` - Returns the last date or timestamp of the week that ends immediately after the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.month_start()` - Returns the first date or timestamp of the month that begins immediately before the specified date or timestamp value in a column or as a literal.
      * `DataFrameColumn.month_begin()` - It is an alias for `DataFrameColumn.month_start()` function.
      * `DataFrameColumn.month_end()` - Returns the last date or timestamp of the month that ends immediately after the specified date or timestamp value in a column or as a literal.
      * `DataFrameColumn.year_start()` - Returns the first date or timestamp of the year that begins immediately before the specified date or timestamp value in a column or as a literal.
      * `DataFrameColumn.year_begin()` - It is an alias for `DataFrameColumn.year_start()` function.
      * `DataFrameColumn.year_end()` - Returns the last date or timestamp of the year that ends immediately after the specified date or timestamp value in a column or as a literal.
      * `DataFrameColumn.quarter_start()` - Returns the first date or timestamp of the quarter that begins immediately before the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.quarter_begin()` - It is an alias for `DataFrameColumn.quarter_start()` function.
      * `DataFrameColumn.quarter_end()` - Returns the last date or timestamp of the quarter that ends immediately after the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.last_sunday()` - Returns the date or timestamp of Sunday that falls immediately before the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.last_monday()` - Returns the date or timestamp of Monday that falls immediately before the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.last_tuesday()` - Returns the date or timestamp of Tuesday that falls immediately before the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.last_wednesday()` - Returns the date or timestamp of Wednesday that falls immediately before specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.last_thursday()`- Returns the date or timestamp of Thursday that falls immediately before specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.last_friday()` - Returns the date or timestamp of Friday that falls immediately before specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.last_saturday()` - Returns the date or timestamp of Saturday that falls immediately before specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.day_of_week()` - Returns the number of days from the beginning of the week to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.day_of_month()` - Returns the number of days from the beginning of the month to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.day_of_year()` - Returns the number of days from the beginning of the year to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.day_of_calendar()` - Returns the number of days from the beginning of the business calendar to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.week_of_month()` - Returns the number of weeks from the beginning of the month to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.week_of_quarter()` - Returns the number of weeks from the beginning of the quarter to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.week_of_year()` - Returns the number of weeks from the beginning of the year to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.week_of_calendar()` - Returns the number of weeks from the beginning of the calendar to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.month_of_year()` - Returns the number of months from the beginning of the year to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.month_of_calendar()` - Returns the number of months from the beginning of the calendar to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.month_of_quarter()` - Returns the number of months from the beginning of the quarter to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.quarter_of_year()` - Returns the number of quarters from the beginning of the year to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.quarter_of_calendar()` - Returns the number of quarters from the beginning of the calendar to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.year_of_calendar()` - Returns the year of the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.day_occurrence_of_month()` - Returns the nth occurrence of the weekday in the month for the date to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.year()` - Returns the integer value for year in the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.month()` - Returns the integer value for month in the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.hour()` - Returns the integer value for hour in the specified timestamp value in a column as a literal.
      * `DataFrameColumn.minute()` - Returns the integer value for minute in the specified timestamp value in a column as a literal.
      * `DataFrameColumn.second()` - Returns the integer value for seconds in the specified timestamp value in a column as a literal.
      * `DataFrameColumn.week()` - Returns the number of weeks from the beginning of the year to the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.next_day()` - Returns the date of the first weekday specified as 'day_value' that is later than the specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.months_between()` - Returns the number of months between value in specified date or timestamp value in a column as a literal and date or timestamp value in argument.
      * `DataFrameColumn.add_months()` - Adds an integer number of months to specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.oadd_months()` - Adds an integer number of months, date or timestamp value in specified date or timestamp value in a column as a literal.
      * `DataFrameColumn.to_date()` - Function converts a string-like representation of a DATE or PERIOD type to Date type.
    * _String Functions_
      * `DataFrameColumn.concat()` - Function to concatenate the columns with a separator.
      * `DataFrameColumn.like()` - Function to match the string pattern. String match is case sensitive. 
      * `DataFrameColumn.ilike()` - Function to match the string pattern. String match is not case sensitive.
      * `DataFrameColumn.substr()` - Returns the substring from a string column.       
      * `DataFrameColumn.startswith()` - Function to check if the column value starts with the specified value or not.       
      * `DataFrameColumn.endswith()` - Function to check if the column value ends with the specified value or not.
      * `DataFrameColumn.format()` - Function to format the values in column based on formatter.
      * `DataFrameColumn.to_char()` - Function converts numeric type or datetype to character type.
      * `DataFrameColumn.trim()` - Function trims the string values in the column.
    * _Regular Arithmetic Functions_
      * `DataFrameColumn.cbrt()` - Computes the cube root of values in the column.
      * `DataFrameColumn.hex()` - Computes the Hexadecimal from decimal for the values in the column.
      * `DataframeColumn.hypot()` - Computes the decimal from Hexadecimal for the values in the column.
      * `DataFrameColumn.unhex()` - computes the hypotenuse for the values between two columns.
    * _Bit Byte Manipulation Functions_
      * `DataFrameColumn.from_byte()` - Encodes a sequence of bits into a sequence of characters.
    * _Comparison Functions_
      * `DataFrameColumn.greatest()` - Returns the greatest values from columns.
      * `DataFrameColumn.least()` - Returns the least values from columns.
    * Behaviour of `DataFrameColumn.replace()` is changed.
    * Behaviour of `DataFrameColumn.to_byte()` is changed. It now decodes a sequence of characters in a given encoding into a sequence of bits.
    * Behaviour of `DataFrameColumn.trunc()` is changed. It now accepts Date type columns.  

* ##### Bug Fixes
  * Argument `url_encode` is no longer used in `create_context()` and is deprecated. 
    * **Important notes**
      * Users do not need to encode password even if password contain special characters.
      * Pass the password to the `create_context()` function argument `password` as it is without changing special characters.
  * `fillna()` in VAL transformation allows to replace NULL values with empty string.

* ##### Updates
  * Support for following deprecated functionality is removed:
    * ML Engine functions
    * STO and APPLY sandbox feature support for testing the script.   
      * sandbox_container_utils is removed. Following methods can no longer be used:
        * `setup_sandbox_env()`
        * `copy_files_from_container()`
        * `cleanup_sandbox_env()`
    * Model Cataloging APIs can no longer be used: 
        * `describe_model()`
        * `delete_model()`
        * `list_models()`
        * `publish_model()`
        * `retrieve_model()`
        * `save_model()`
  * `DataFrame.join()`
    * Arguments `lsuffix` and `rsuffix` now add suffixes to new column names for join operation.
  * `DataFrame.describe()`
    * New argument `columns` is added to generate statistics on only those columns instead of all applicable columns.
  * `DataFrame.groupby()`
    * Supports `CUBE` and `ROLLUP` with additional optional argument `option`.
  * `DataFrame.column.window()` 
    * Supports ColumnExpressions for `partition_columns` and `order_columns` arguments.
  * `DataFrame.column.contains()` allows ColumnExpressions for `pattern` argument.
  * `DataFrame.window()` 
    * Supports ColumnExpressions for `partition_columns` and `order_columns` arguments.

#### teradataml 17.20.00.07
* ##### New Features/Functionality
  * ###### Open Analytics Framework (OpenAF) APIs:
      * Manage all user environments.
        * `create_env()`:
          * new argument `conda_env` is added to create a conda environment.
        * `list_user_envs()`:
          * User can list conda environment(s) by using filter with new argument `conda_env`.
      *  Conda environment(s) can be managed using APIs for installing , updating, removing files/libraries. 
* ##### Bug Fixes
  * `columns` argument for `FillNa` function is made optional.

#### teradataml 17.20.00.06
* ##### New Features/Functionality
* ###### teradataml DataFrameColumn a.k.a. ColumnExpression
    * `ColumnExpression.nulls_first()` - Displays NULL values at first.
    * `ColumnExpression.nulls_last()` - Displays NULL values at last.
    * _Bit Byte Manipulation Functions_
      * `DataFrameColumn.bit_and()` - Returns the logical AND operation on the bits from
         the column and corresponding bits from the argument.
      * `DataFrameColumn.bit_get()` - Returns the bit specified by input argument from the column and 
         returns either 0 or 1 to indicate the value of that bit.
      * `DataFrameColumn.bit_or()` - Returns the logical OR operation on the bits from the column and 
         corresponding bits from the argument.
      * `DataFrameColumn.bit_xor()` - Returns the bitwise XOR operation on the binary representation of the
         column and corresponding bits from the argument.
      * `DataFrameColumn.bitand()` - It is an alias for `DataFrameColumn.bit_and()` function.
      * `DataFrameColumn.bitnot()` - Returns a bitwise complement on the binary representation of the column.
      * `DataFrameColumn.bitor()` - It is an alias for `DataFrameColumn.bit_or()` function.
      * `DataFrameColumn.bitwise_not()` - It is an alias for `DataFrameColumn.bitnot()` function.
      * `DataFrameColumn.bitwiseNOT()` - It is an alias for `DataFrameColumn.bitnot()` function.
      * `DataFrameColumn.bitxor()` - It is an alias for `DataFrameColumn.bit_xor()` function.
      * `DataFrameColumn.countset()` - Returns the count of the binary bits within the column that are either set to 1 
         or set to 0, depending on the input argument value.
      * `DataFrameColumn.getbit()` - It is an alias for `DataFrameColumn.bit_get()` function.
      * `DataFrameColumn.rotateleft()` - Returns an expression rotated to the left by the specified number of bits,
         with the most significant bits wrapping around to the right.
      * `DataFrameColumn.rotateright()` - Returns an expression rotated to the right by the specified number of bits,
         with the least significant bits wrapping around to the left.
      * `DataFrameColumn.setbit()` - Sets the value of the bit specified by input argument to the value
         of column.
      * `DataFrameColumn.shiftleft()` - Returns the expression when value in column is shifted by the specified
         number of bits to the left.
      * `DataFrameColumn.shiftright()` - Returns the expression when column expression is shifted by the specified
         number of bits to the right.
      * `DataFrameColumn.subbitstr()` - Extracts a bit substring from the column expression based on the specified 
         bit position.
      * `DataFrameColumn.to_byte()` - Converts a numeric data type to the Vantage byte representation
        (byte value) of the column expression value.
      
    * _Regular Expression Functions_
      * `DataFrameColumn.regexp_instr()` - Searches string value in column for a match to value specified in argument.
      * `DataFrameColumn.regexp_replace()` - Replaces the portions of string value in a column that matches the value 
         specified regex string and replaces with the replace string.
      * `DataFrameColumn.regexp_similar()` - Compares value in column to value in argument and returns integer value.
      * `DataFrameColumn.regexp_substr()` - Extracts a substring from column that matches a regular expression 
         specified in the input argument.

* ###### Open Analytics Framework (OpenAF) APIs:
    * Manage all user environments.
      * `create_env()`:
        * User can create one or more user environments using newly added argument `template` by providing specifications in template json file. New feature allows user to create complete user environment, including file and library installation, in just single function call.
    * UserEnv Class – Manage individual user environment.
      * Properties:
        * `models` - Supports listing of models in user environment.
      * Methods:
        * `install_model()` - Install a model in user environment.
        * `uninstall_model()` - Uninstall a model from user environment.
        * `snapshot()`- Take the snapshot of the user environment.

* ###### teradataml: Bring Your Own Model
    * _New Functions_
      * `DataRobotPredict()` - Score the data in Vantage using the model trained externally in datarobot and stored 
                               in Vantage.

* ##### Updates
  * `DataFrame.describe()`
    * Method now accepts an argument `statistics`, which specifies the aggregate operation to be performed. 
  * `DataFrame.sort()` 
    * Method now accepts ColumnExpressions as well.
    * Enables sorting using NULLS FIRST and NULLS LAST.
  * `view_log()` downloads the Apply query logs based on query id.
  * Arguments which accepts floating numbers will accept integers also for `Analytics Database Analytic Functions`.
  * Argument `ignore_nulls` added to `DataFrame.plot()` to ignore the null values while plotting the data.
  * `Dataframe.sample()` 
    * Method supports column stratification. 
    
* ##### Bug Fixes
  * `DataFrameColumn.cast()` accepts all teradatasqlalchemy types.
  * Minor bug fix related to `DataFrame.merge()`.

#### teradataml 17.20.00.05
* ##### New Features/Functionality
  * ###### teradataml: Hyperparameter-Tuning - Technique to identify best model parameters.
    Hyperparameter tuning is an optimization method to determine the optimal set of 
    hyperparameters for the given dataset and learning model. teradataml hyperparameter tuning feature
    offers best model identification, parallel execution, early stopping feature, best data identification, 
    model evaluation, model prediction, live logging, input data hyper-parameterization, input data sampling, 
    numerous scoring functions, hyper-parameterization for non-model trainer functions.  
    * `GridSearch`
      GridSearch is an exhaustive search algorithm that covers all possible
      parameter values to identify optimal hyperparameters.
      * Methods of GridSearch
        * `__init__()` - Instantiate an object of GridSearch for given model function and parameters.
        * `evaluate()` - Function to perform evaluation on the given teradataml DataFrame using default model.
        * `fit()` - Function to perform hyperparameter-tuning for given hyperparameters and model on teradataml DataFrame.
        * `get_error_log()` - Useful to get the error log if model execution failed, using the model identifier.
        * `get_input_data()` - Useful to get the input data using the data identifier, when input data is also parameterized.
        * `get_model()` - Returns the trained model for the given model identifier.
        * `get_parameter_grid()` - Returns the hyperparameter space used for hyperparameter optimization.
        * `is_running()` - Returns the execution status of hyperaparameter tuning.
        * `predict()` - Function to perform prediction on the given teradataml DataFrame using default model.
        * `set_model()` -  Function to update the default model.
      * Properties of GridSearch
        * `best_data_id` - Returns the best data identifier used for model training.
        * `best_model` - Returns the best trained model.
        * `best_model_id` - Returns the identifier for best model.
        * `best_params_` - Returns the best set of hyperparameter.
        * `best_sampled_data_` - Returns the best sampled data used to train the best model.
        * `best_score_` - Returns the best trained model score.
        * `model_stats` - Returns the model evaluation reports.
        * `models` - Returns the metadata of all the models.
    * `RandomSearch`
      RandomSearch algorithm performs random sampling on hyperparameter 
      space to identify optimal hyperparameters.
      * Methods of RandomSearch
        * `__init__()` - Instantiate an object of RandomSearch for given model function and parameters.
        * `evaluate()` - Function to perform evaluation on the given teradataml DataFrame using default model.
        * `fit()` - Function to perform hyperparameter-tuning for given hyperparameters and model on teradataml DataFrame.
        * `get_error_log()` - Useful to get the error log if model execution failed, using the model identifier.
        * `get_input_data()` - Useful to get the input data using the data identifier, when input data is also parameterized.
        * `get_model()` - Returns the trained model for the given model identifier.
        * `get_parameter_grid()` - Returns the hyperparameter space used for hyperparameter optimization.
        * `is_running()` - Returns the execution status of hyperaparameter tuning.
        * `predict()` - Function to perform prediction on the given teradataml DataFrame using default model.
        * `set_model()` - Function to update the default model.
      * Properties of GridSearch    
        * `best_data_id` - Returns the best data identifier used for model training.
        * `best_model` - Returns the best trained model.
        * `best_model_id` - Returns the identifier for best model.
        * `best_params_` - Returns the best set of hyperparameter.
        * `best_sampled_data_` - Returns the best sampled data used to train the best model.
        * `best_score_` - Returns the best trained model score.
        * `model_stats` - Returns the model evaluation reports.
        * `models` - Returns the metadata of all the models.
  
  * ###### teradataml: Analytic Functions
    teradataml currently has different functions to generate a model, predict, transform and evaluate. All these functions are needed to be invoked individually, i.e., predict(), evaluate(), transform() cannot be invoked using the model trainer function output. Enhancement done to this feature now enables user to invoke these functions as methods of the model trainer function. Below is the list of functions, updated with this enhancement:
    * Analytics Database Analytic Functions
      *  `BincodeFit()` - Supports `transform()` method.
      *  `DecisionForest()` - Supports `predict()`, `evaluate()` methods.
      *  `Fit()` - Supports `transform()` method. 
      *  `GLM()` - Supports `predict()`, `evaluate()` methods. 
      *  `GLMPerSegment()` - Supports `predict()`, `evaluate()` methods. 
      *  `KMeans()` - Supports `predict()` method.
      *  `KNN()` - Supports `predict()`, `evaluate()` methods. 
      *  `NaiveBayesTextClassifierTrainer()` - Supports `predict()`, `evaluate()` methods. 
      *  `NonLinearCombineFit()` - Supports `transform()` method. 
      *  `OneClassSVM()` - Supports `predict()` method.
      *  `OneHotEncodingFit()` - Supports `transform()` method. 
      *  `OrdinalEncodingFit()` - Supports `transform()` method. 
      *  `OutlierFilterFit()` - Supports `transform()` method. 
      *  `PolynomialFeaturesFit()` - Supports `transform()` method. 
      *  `RandomProjectionFit()` - Supports `transform()` method. 
      *  `RowNormalizeFit()` - Supports `transform()` method. 
      *  `ScaleFit()` - Supports `transform()` method. 
      *  `SimpleImputeFit()` - Supports `transform()` method. 
      *  `SVM()` - Supports `predict()`, `evaluate()` methods. 
      *  `TargetEncodingFit()` - Supports `transform()` method. 
      *  `XGBoost()` - Supports `predict()`, `evaluate()` methods. 
    * Time Series Analytic (UAF) Functions
      *  `ArimaEstimate()` - Supports `forecast()`, `validate()` methods.
      *  `DFFT()` - Supports `convolve()`, `inverse()` methods. 
      *  `IDFFT()` - Supports `inverse()` method. 
      *  `DFFT2()` - Supports `convolve()`, `inverse()` methods. 
      *  `IDFFT2()` - Supports `inverse()` method. 
      *  `DIFF()` - Supports `inverse()` method. 
      *  `UNDIFF()` - Supports `inverse()` method. 
      *  `SeasonalNormalize()` - Supports `inverse()` method.

  * ###### teradataml: DataFrame
    * New Functions
      * `DataFrame.plot()` - Generates the below type of plots on teradataml DataFrame.
        * line - Generates line plot.
        * bar - Generates bar plot.
        * scatter - Generates scatter plot.
        * corr - Generates correlation plot.
        * wiggle - Generates a wiggle plot.
        * mesh - Generates a mesh plot.
      * `DataFrame.itertuples()` - iterate over teradataml DataFrame rows as namedtuples or list.
  * ###### teradataml: GeoDataFrame
    * New Functions
      * `GeoDataFrame.plot()` - Generate the below type of plots on teradataml GeoDataFrame.
        * line - Generates line plot.
        * bar - Generates bar plot.
        * scatter - Generates scatter plot.
        * corr - Generates correlation plot.
        * wiggle - Generates a wiggle plot.
        * mesh - Generates a mesh plot.
        * geometry - Generates plot on geospatial data. 
  * Plot:
    * `Axis` - Genertes the axis for plot.
    * `Figure` - Generates the figure for plot.
    * `subplots` - Helps in generating multiple plots on a single `Figure`.    
  * Bring Your Own Model (BYOM) Function:
    * `DataikuPredict` - Score the data in Vantage using the model trained externally in Dataiku UI and stored in Vantage.
  * `async_run_status()` - Function to check the status of asynchronous run(s) using unique run id(s).
  
  * ###### teradataml DataFrameColumn a.k.a. ColumnExpression
    * _Regular Arithmetic Functions_
      * `DataFrameColumn.abs()` - Computes the absolute value.
      * `DataFrameColumn.ceil()` - Returns the ceiling value of the column.
      * `DataFrameColumn.ceiling()` - It is an alias for `DataFrameColumn.ceil()` function.
      * `DataFrameColumn.degrees()` - Converts radians value from the column to degrees.
      * `DataFrameColumn.exp()` - Raises e (the base of natural logarithms) to the power of the value in the column, where e = 2.71828182845905.
      * `DataFrameColumn.floor()` - Returns the largest integer equal to or less than the value in the column.
      * `DataFrameColumn.ln()` - Computes the natural logarithm of values in column.
      * `DataFrameColumn.log10()` - Computes the base 10 logarithm.
      * `DataFrameColumn.mod()` - Returns the modulus of the column.
      * `DataFrameColumn.pmod()` - It is an alias for `DataFrameColumn.mod()` function.
      * `DataFrameColumn.nullifzero()` - Converts data from zero to null to avoid problems with division by zero.
      * `DataFrameColumn.pow()` - Computes the power of the column raised to expression or constant.
      * `DataFrameColumn.power()` - It is an alias for `DataFrameColumn.pow()` function.
      * `DataFrameColumn.radians()` - Converts degree value from the column to radians.
      * `DataFrameColumn.round()` - Returns the rounded off value.
      * `DataFrameColumn.sign()` - Returns the sign.
      * `DataFrameColumn.signum()` - It is an alias for `DataFrameColumn.sign()` function.
      * `DataFrameColumn.sqrt()` - Computes the square root of values in the column.
      * `DataFrameColumn.trunc()` - Provides the truncated value of columns.
      * `DataFrameColumn.width_bucket()` - Returns the number of the partition to which column is assigned.
      * `DataFrameColumn.zeroifnull()` - Converts data from null to zero to avoid problems with null.
    * _Trigonometric Functions_
      * `DataFrameColumn.acos()` - Returns the arc-cosine value.
      * `DataFrameColumn.asin()` - Returns the arc-sine value.
      * `DataFrameColumn.atan()` - Returns the arc-tangent value.
      * `DataFrameColumn.atan2()` - Returns the arc-tangent value based on x and y coordinates.
      * `DataFrameColumn.cos()` - Returns the cosine value.
      * `DataFrameColumn.sin()` - Returns the sine value.
      * `DataFrameColumn.tan()` - Returns the tangent value.
    * _Hyperbolic Functions_
      * `DataFrameColumn.acosh()` - Returns the inverse hyperbolic cosine value. 
      * `DataFrameColumn.asinh()` - Returns the inverse hyperbolic sine value.
      * `DataFrameColumn.atanh()` - Returns the inverse hyperbolic tangent value.
      * `DataFrameColumn.cosh()` - Returns the hyperbolic cosine value.
      * `DataFrameColumn.sinh()` - Returns the hyperbolic sine value
      * `DataFrameColumn.tanh()` - Returns the hyperbolic tangent value.
    * _String Functions_
      * `DataFrameColumn.ascii()` - Returns the decimal representation of the first character in column.
      * `DataFrameColumn.char2hexint()` - Returns the hexadecimal representation for a character string in a column.
      * `DataFrameColumn.chr()` - Returns the Latin ASCII character of a given a numeric code value in column.
      * `DataFrameColumn.char()` - It is an alias for `DataFrameColumn.chr()` function.
      * `DataFrameColumn.character_length()` - Returns the number of characters in the column.
      * `DataFrameColumn.char_length()` - It is an alias for `DataFrameColumn.character_length()` function.
      * `DataFrameColumn.edit_distance()` - Returns the minimum number of edit operations required to 
         transform string in a column into string specified in argument.
      * `DataFrameColumn.index()` - Returns the position of a string in a column where string specified in argument starts.
      * `DataFrameColumn.initcap()` - Modifies a string column and returns the string with the first character
         of each word in uppercase.
      * `DataFrameColumn.instr()` - Searches the string in a column for occurrences of search string passed as argument.
      * `DataFrameColumn.lcase()` - Returns a character string identical to string values in column,
         with all uppercase letters replaced with their lowercase equivalents.
      * `DataFrameColumn.left()` - Truncates string in a column to a specified number of characters desired from
         the left side of the string.
      * `DataFrameColumn.length()` - It is an alias for `DataFrameColumn.character_length()` function.
      * `DataFrameColumn.levenshtein()` - It is an alias for `DataFrameColumn.edit_distance()` function.
      * `DataFrameColumn.locate()` - Returns the position of the first occurrence of a string in a column within 
         string in argument. 
      * `DataFrameColumn.lower()` - It is an alias for `DataFrameColumn.character_lcase()` function.
      * `DataFrameColumn.lpad()` - Returns the string in a column padded to the left with the characters specified 
         in argument so that the resulting string has length specified in argument.
      * `DataFrameColumn.ltrim()` - Returns the string in a column, with its left-most characters removed up
        to the first character that is not in the string specified in argument.
      * `DataFrameColumn.ngram()` - Returns the number of n-gram matches between string in a column,
        and string specified in argument.
      * `DataFrameColumn.nvp()` - Extracts the value of a name-value pair where the name in the pair matches
        the name and the number of the occurrence specified.
      * `DataFrameColumn.oreplace()` - Replaces every occurrence of search string in the column.
      * `DataFrameColumn.otranslate()` - Returns string in a column with every occurrence of each character in
         string in argument replaced with the corresponding character in another argument.
      * `DataFrameColumn.replace()` - It is an alias for `DataFrameColumn.oreplace()` function.
      * `DataFrameColumn.reverse()` - Returns the reverse of string in column.
      * `DataFrameColumn.right()` - Truncates input string to a specified number of characters desired from
         the right side of the string.
      * `DataFrameColumn.rpad()` - Returns the string in a column padded to the right with the characters specified 
         in argument so the resulting string has length specified in argument.
      * `DataFrameColumn.rtrim()` - Returns the string in column, with its right-most characters removed up
         to the first character that is not in the string specified in argument.
      * `DataFrameColumn.soundex()` - Returns a character string that represents the Soundex code for
         string in a column.
      * `DataFrameColumn.string_cs()` - Returns a heuristically derived integer value that can be used to determine
         which KANJI1-compatible client character set was used to encode string in a column.
      * `DataFrameColumn.translate()` - It is an alias for `DataFrameColumn.otranslate()` function.
      * `DataFrameColumn.upper()` - Returns a character string with all lowercase letters in a column replaced 
         with their uppercase equivalents.

  * ##### teradataml Options
    * Configuration Options
      * `configure.indb_install_location`
        Specifies the installation location of In-DB Python package.
  
* ##### Updates
  * Open Analytics Framework (OpenAF) APIs:
    * `set_auth_token()`
      * `set_auth_token()` does not accept username and password anymore. Instead, function opens up a browser session and user should authenticate in browser.
      * After token expiry, teradataml will open a browser and user needs to authenticate again.
      * If client machine does not have browser, then user should copy the URL posted by teradataml and authenticate themselves.
    * Security fixes - `auth_token` is not set or retrieved from the `configure` option anymore.
    * Manage all user environments.
      * `create_env()` - supports creation of R environment.
      * `remove_env()` - Supports removal of remote R environment.
      * `remove_all_envs()` - Supports removal of all remote R environments.
      * `remove_env()` and `remove_all_envs()` supports asynchronous call.
    * UserEnv Class – Supports managing of R remote environments.
      * Properties:
        * `libs` - Supports listing of libraries in R remote environment.
      * Methods:
        * `install_lib()` - Supports installing of libraries in remote R environment.
        * `uninstall_lib()` - Supports uninstalling of libraries in remote R environment.
        * `update_lib()` - Supports updating of libraries in remote R environment.
  * Unbounded Array Framework (UAF) Functions:
    * `ArimaEstimate()`
        * Added support for `CSS` algorithm via `algorithm` argument.

* ##### Bug Fixes
    * Installation location of In-DB 2.0.0 package is changed. Script() will now work with both 2.0.0 and previous version.  

## Release Notes:
#### teradataml 17.20.00.04
* ##### New Features/Functionality
  * teradataml is now compatible with SQLAlchemy 2.0.X
    * **Important notes** when user has sqlalchemy version >= 2.0: 
      * Users will not be able to run the `execute()` method on SQLAlchemy engine object returned by 
        `get_context()` and `create_context()` teradataml functions. This is due to the SQLAlchemy has
        removed the support for `execute()` method on the engine object. Thus, user scripts where 
        `get_context().execute()` and `create_context().execute()`, is used, Teradata recommends to
        replace those with either `execute_sql()` function exposed by teradataml or `exec_driver_sql()` 
        method on the `Connection` object returned by `get_connection()` function in teradataml.
      * Now `get_connection().execute()` accepts only executable sqlalchemy object. Refer to 
        `sqlalchemy.engine.base.execute()` for more details.
      * Teradata recommends to use either `execute_sql()` function exposed by teradataml or 
        `exec_driver_sql()` method on the `Connection` object returned by `get_connection()` 
        function in teradataml, in such cases.
  * New utility function `execute_sql()` is added to execute the SQL.  
  * Extending compatibility for MAC with ARM processors.
  * Added support for floor division (//) between two teradataml DataFrame Columns.
  * Analytics Database Analytic Functions:
    * `GLMPerSegment()`
    * `GLMPredictPerSegment()`
    * `OneClassSVM()`
    * `OneClassSVMPredict()`
    * `SVM()`
    * `SVMPredict()`
    * `TargetEncodingFit()`
    * `TargetEncodingTransform()`
    * `TrainTestSplit()`
    * `WordEmbeddings()`
    * `XGBoost()`
    * `XGBoostPredict()`
    
  * ###### teradataml Options
    * Display Options
      * `display.geometry_column_length`
        Option to display the default length of geometry column in GeoDataFrame.
        
  * ##### Updates
    * `set_auth_token()` function can generate the client id automatically based on org_id when user do not specify it.
    * Analytics Database Analytic Functions:
      * `ColumnTransformer()` 
          * Does not allow list values for arguments - `onehotencoding_fit_data` and `ordinalencoding_fit_data`.
      * `OrdidnalEncodingFit()`
          * New arguments added - `category_data`, `target_column_names`, `categories_column`, `ordinal_values_column`.
          * Allows the list of values for arguments - `target_column`, `start_value`, `default_value`.
      * `OneHotEncodingFit()`
          * New arguments added - `category_data`, `approach`, `target_columns`, `categories_column`, `category_counts`.
          * Allows the list of values for arguments - `target_column`, `other_column`.

  * ##### Bug Fixes
    * `DataFrame.sample()` method output is now deterministic.
    * `copy_to_sql()` now preserves the rows of the table even when the view content is copied to the same table name.
    * `list_user_envs()` does not raise warning when no user environments found.

## Release Notes:
#### teradataml 17.20.00.03

  * ##### Updates
    * DataFrame.join 
      * New arguments `lprefix` and `rprefix` added.
      * Behavior of arguments `lsuffix` and `rsuffix` will be changed in future, use new arguments instead.
      * New and old affix arguments can now be used independently.
    * Analytic functions can be imported regardless of context creation. 
      Import after create context constraint is now removed.
    * `ReadNOS` and `WriteNOS` now accept dictionary value for `authorization` and `row_format` arguments.
    * `WriteNOS` supports writing CSV files to external store.
    * Following model cataloging APIs will be deprecated in future:
       * describe_model
       * delete_model
       * list_models
       * publish_model
       * retrieve_model
       * save_model
  
  * ##### Bug Fixes
    * `copy_to_sql()` bug related to NaT value has been fixed.
    * Tooltip on PyCharm IDE now points to SQLE.
    * `value` argument of `FillNa()`, a Vantage Analytic Library function supports special characters.
    * `case` function accepts DataFrame column as value in `whens` argument.

## Release Notes:
#### teradataml 17.20.00.02
* ##### New Features/Functionality
  * ###### teradataml: Open Analytics
    * New Functions
      * `set_auth_token()` - Sets the JWT token automatically for using Open AF API's.
    
  * ###### teradataml Options
    * Display Options
      * `display.suppress_vantage_runtime_warnings`
        Suppresses the VantageRuntimeWarning raised by teradataml, when set to True.

  * ##### Updates
    * SimpleImputeFit function arguments `stats_columns` and `stats` are made to be optional.
    * New argument `table_format` is added to ReadNOS().
    * Argument `full_scan` is changed to `scan_pct` in ReadNOS(). 
  
  * ##### Bug Fixes
    * Minor bug fix related to read_csv.
    * APPLY and `DataFrame.apply()` supports hash by and local order by.
    * Output column names are changed for DataFrame.dtypes and DataFrame.tdtypes.

## Release Notes:
#### teradataml 17.20.00.01
* ##### New Features/Functionality
  * ###### teradataml: DataFrame
    * New Functions
      * `DataFrame.pivot()` - Rotate data from rows into columns to create easy-to-read DataFrames.
      * `DataFrame.unpivot()` - Rotate data from columns into rows to create easy-to-read DataFrames.
      * `DataFrame.drop_duplicate()` - Drop duplicate rows from teradataml DataFrame.
    * New properties 
      * `Dataframe.is_art` - Check whether teradataml DataFrame is created on an Analytic Result Table, i.e., ART table or not.

  * ###### teradataml:  Unbounded Array Framework (UAF) Functions:
    * New Functions
      * New Functions Supported on Database Versions: 17.20.x.x
        * MODEL PREPARATION AND PARAMETER ESTIMATION functions:
			 1. `ACF()`
			 2. `ArimaEstimate()`
			 3. `ArimaValidate()`
			 4. `DIFF()`
			 5. `LinearRegr()`
			 6. `MultivarRegr()`
			 7. `PACF()`
			 8. `PowerTransform()`
			 9. `SeasonalNormalize()`
			 10. `Smoothma()`
			 11. `UNDIFF()`
			 12. `Unnormalize()`
		* SERIES FORECASTING functions:
			 1. `ArimaForecast()`
			 2. `DTW()`
			 3. `HoltWintersForecaster()`
			 4. `MAMean()`
			 5. `SimpleExp()`
		* DATA PREPARATION functions:
			 1. `BinaryMatrixOp()`
			 2. `BinarySeriesOp()`
			 3. `GenseriesFormula()`
			 4. `MatrixMultiply()`
			 5. `Resample()`
		* DIAGNOSTIC STATISTICAL TEST functions:
			 1. `BreuschGodfrey()`
			 2. `BreuschPaganGodfrey()`
			 3. `CumulPeriodogram()`
			 4. `DickeyFuller()`
			 5. `DurbinWatson()`
			 6. `FitMetrics()`
			 7. `GoldfeldQuandt()`
			 8. `Portman()`
			 9. `SelectionCriteria()`
			 10. `SignifPeriodicities()`
			 11. `SignifResidmean()`
			 12. `WhitesGeneral()`
		* TEMPORAL AND SPATIAL functions:
			 1. `Convolve()`
			 2. `Convolve2()`
			 3. `DFFT()`
			 4. `DFFT2()`
			 5. `DFFT2Conv()`
			 6. `DFFTConv()`
			 7. `GenseriesSinusoids()`
			 8. `IDFFT()`
			 9. `IDFFT2()`
			 10. `LineSpec()`
			 11. `PowerSpec()`
		* GENERAL UTILITY functions:
			 1. `ExtractResults()`
			 2. `InputValidator()`
			 3. `MInfo()`
			 4. `SInfo()`
			 5. `TrackingOp()`
        
    * New Features: Inputs to Unbounded Array Framework (UAF) functions
      * `TDAnalyticResult()` - Allows to prepare function output generated by UAF functions to be passed.
      * `TDGenSeries()` - Allows to generate a series, that can be passed to a UAF function.
      * `TDMatrix()` - Represents a Matrix in time series, that can be created from a teradataml DataFrame.
      * `TDSeries()` - Represents a Series in time series, that can be created from a teradataml DataFrame.

  * ##### Updates 
    * Native Object Store (NOS) functions support authorization by specifying authorization object.
    * `display_analytic_functions()` categorizes the analytic functions based on function type.
    * ColumnTransformer accepts multiple values for arguments nonlinearcombine_fit_data, 
      onehotencoding_fit_data, ordinalencoding_fit_data.
  
  * ##### Bug Fixes
    * Redundant warnings thrown by teradataml are suppressed.
    * OpenAF supports when context is created with JWT Token.
    * New argument "match_column_order" added to copy_to_sql, that allows DataFrame loading with any column order.
    * `copy_to_sql` updated to map data type timezone(tzinfo) to TIMESTAMP(timezone=True), instead of VARCHAR.
    * Improved performance for DataFrame.sum and DataFrameColumn.sum functions.

## Release Notes:
#### teradataml 17.20.00.00
* ##### New Features/Functionality
  * ###### teradataml: Analytics Database Analytic Functions
    * _New Functions_ 
      * ###### New Functions Supported on Database Versions: 17.20.x.x
        * `ANOVA()`​
        * `ClassificationEvaluator()`​
        * `ColumnTransformer()`​
        * `DecisionForest()`
        * `GLM​()`
        * `GetFutileColumns()`
        * `KMeans()`​
        * `KMeansPredict()`​​
        * `NaiveBayesTextClassifierTrainer()`​
        * `NonLinearCombineFit()`​
        * `NonLinearCombineTransform()`​
        * `OrdinalEncodingFit​()`
        * `OrdinalEncodingTransform()`​
        * `RandomProjectionComponents​()`
        * `RandomProjectionFit​()`
        * `RandomProjectionTransform()`​
        * `RegressionEvaluator​()`
        * `ROC​()`
        * `SentimentExtractor()`​
        * `Silhouette​()`
        * `TDGLMPredict​()`
        * `TextParser​()`
        * `VectorDistance()`
    * _Updates_
      * `display_analytic_functions()` categorizes the analytic functions based on function type.
      * Users can provide range value for columns argument.
 
  * ###### teradataml: Open Analytics
    * Manage all user environments.
      * `list_base_envs()` - list the available python base versions.​
      * `create_env()` - create a new user environment. ​
      * `get_env()` - get existing user environment.
      * `list_user_envs()` - list the available user environments.​
      * `remove_env()` - delete user environment.​
      * `remove_all_envs()` - delete all the user environments.
    * UserEnv Class – Manage individual user environment.      
      * Properties
        * `files` - Get files in user environment. 
        * `libs` - Get libraries in user environment.
      * Methods
        * `install_file()` - Install a file in user environment.​
        * `remove_file()` - Remove a file in user environment.​
        * `install_lib()` - Install a library in user environment.​
        * `update_lib()` - Update a library in user environment.​
        * `uninstall_lib()` - Uninstall a library in user environment.​
        * `status()` - Check the status of​
          * file installation​
          * library installation​
          * library update​
          * library uninstallation​
        * `refresh()` - Refresh the environment details in local client.
    * Apply Class – Execute a user script on VantageCloud Lake.​
      * `__init__()` - Instantiate an object of apply for script execution.​
      * `install_file()` - Install a file in user environment.​
      * `remove_file()` - Remove a file in user environment.​
      * `set_data()` – Reset data and related arguments.​
      * `execute_script()` – Executes Python script.
  
  * ###### teradataml: DataFrame
    * _New Functions_
      * `DataFrame.apply()` - Execute a user defined Python function on VantageLake Cloud.

  * ###### teradataml: Bring Your Own Model
    * _New Functions_
      * `ONNXPredict()` - Score using model trained externally on ONNX and stored in Vantage.

  * ###### teradataml: Options
    * _New Functions_
      * set_config_params() New API to set all config params in one go.
    * _New Configuration Options_
      * For Open Analytics support.​
        * ues_url – User Environment Service URL for VantageCloud Lake.​
        * auth_token – Authentication token to connect to VantageCloud Lake.
        * certificate_file – Path to a CA_BUNDLE file or directory with certificates of trusted CAs.

  * ##### Updates
    * `accumulate` argument is working for `ScaleTransform()`.
    * Following functions have `accumulate` argument added on Database Versions: 17.20.x.x
      * `ConvertTo()`
      * `GetRowsWithoutMissingValues()`
      * `GetRowsWithoutMissingValues()`
    * `OutlierFilterFit()` supports multiple output.
    * For `OutlierFilterFit()` function below arguments are optional in teradataml 17.20.x.x
      * `lower_percentile`
      * `upper_percentile`
      * `outlier_method`
      * `replacement_value`
      * `percentile_method`
    * Analytics Database analytic functions – In line help, i.e., help() for the functions
    is available.​
    
  * ##### Bug Fixes
    * Vantage Analytic Library FillNa() function: Now `columns` argument is required.
    * `output_responses` argument in MLE function `DecisionTreePredict()`, does not allow empty string.
    * teradataml closes docker sandbox environment properly.
    * Users can create context using JWT token.

#### teradataml 17.10.00.02
* ##### New Features/Functionality
  * ###### Database Utility
      * `list_td_reserved_keywords()` - Validates if the specified string is Teradata reserved
        keyword or not, else lists down all the Teradata reserved keywords.

* ##### Updates
    * ###### DataFrame
      * _Updates_
        * Multiple columns can be selected using slice operator ([]).

    * ###### Script
      * _Updates_
        * A warning will be raised, when Teradata reserved keyword is used in Script local mode.
        
* ##### Bug Fixes
  * Numeric overflow issue observed for describe(), sum(), csum(), and mean() has been fixed.
  * Error messages are updated for SQLE function arguments accepting multiple datatypes.
  * Error messages are updated for SQLE function arguments volatile and persist arguments when 
    non-boolean value is provided.
  * DataFrame sample() method can handle column names with special characters like space, hyphen, 
    period etc.
  * In-DB SQLE functions can be loaded for any locale setting.
  * `create_context()` - Password containing special characters requires URL encoding as per
    https://docs.microfocus.com/OMi/10.62/Content/OMi/ExtGuide/ExtApps/URL_encoding.html. 
    teradataml has added a fix to take care of the URL encoding of the password while creating a context. 
    Also, a new argument is added to give a more control over the URL encoding to be done at the time of context creation.

#### teradataml 17.10.00.01
* ##### New Features/Functionality
  * ###### Geospatial
    The Geospatial feature in teradataml enables data manipulation, exploration and analysis on tables, views, and queries on Teradata Vantage that contains Geospatial data.
    * ###### Geomtery Types
      * Point
      * LineString
      * Polygon
      * MultiPoint
      * MultiLineString
      * MultiPolygon
      * GeometryCollection
      * GeoSequence
    * ###### teradataml GeoDataFrame
      * Properties
        * columns
        * dtypes
        * geometry
        * iloc
        * index
        * loc
        * shape
        * size
        * tdtypes
        * Geospatial Specific Properties
          * ###### Properties for all Types of Geometries
            * boundary
            * centroid
            * convex_hell
            * coord_dim
            * dimension
            * geom_type
            * is_3D
            * is_empty
            * is_simple
            * is_valid
            * max_x
            * max_y
            * max_z
            * min_x
            * min_y
            * min_z
            * srid
          * ###### Properties for Point Geometry
            * x
            * y
            * z
          * ###### Properties for LineString Geometry
            * is_closed_3D
            * is_closed
            * is_ring
          * ###### Properties for Polygon Geometry
            * area
            * exterior
            * perimeter
      * Methods
        * `__getattr__()`
        * `__getitem__()`
        * `__init__()`
        * `__repr__()`
        * `assign()`
        * `concat()`
        * `count()`
        * `drop()`
        * `dropna()`
        * `filter()`
        * `from_query()`
        * `from_table()`
        * `get()`
        * `get_values()`
        * `groupby()`
        * `head()`
        * `info()`
        * `join()`
        * `keys()`
        * `merge()`
        * `sample()`
        * `select()`
        * `set_index()`
        * `show_query()`
        * `sort()`
        * `sort_index()`
        * `squeeze()`
        * `tail()`
        * `to_csv()`
        * `to_pandas()`
        * `to_sql()` 
        * Geospatial Specific Methods
          * ###### Methods for All Type of Geometry
            * `buffer()`
            * `contains()`
            * `crosses()`
            * `difference()`
            * `disjoint()`
            * `distance()`
            * `distance_3D()`
            * `envelope()`
            * `geom_equals()`
            * `intersection()`
            * `intersects()`
            * `make_2D()`
            * `mbb()`
            * `mbr()`
            * `overlaps()`
            * `relates()`
            * `set_exterior()`
            * `set_srid()`
            * `simplify()`
            * `sym_difference()`
            * `to_binary()`
            * `to_text()`
            * `touches()`
            * `transform()`
            * `union()`
            * `within()`
            * `wkb_geom_to_sql()`
            * `wkt_geom_to_sql()`
          * ###### Methods for Point Geometry
            * `spherical_buffer()`
            * `spherical_distance()`
            * `spheriodal_buffer()`
            * `spheriodal_distance()`
            * `set_x()`
            * `set_y()`
            * `set_z()`
          * ###### Methods for LineString Geometry
            * `end_point()`
            * `length()`
            * `length_3D()`
            * `line_interpolate_point()`
            * `num_points()`
            * `point()`
            * `start_point()`
          * ###### Methods for Polygon Geometry
            * `interiors()`
            * `num_interior_ring()`
            * `point_on_surface()`
          * ###### Methods for GeometryCollection Geometry
            * `geom_component()`
            * `num_geometry()`
          * ###### Methods for GeoSequence Geometry
            * `clip()`
            * `get_final_timestamp()`
            * `get_init_timestamp()`
            * `get_link()`
            * `get_user_field()`
            * `get_user_field_count()`
            * `point_heading()`
            * `set_link()`
            * `speed()`
          * ###### Filtering Functions and Methods
            * `intersects_mbb()`
            * `mbb_filter()`
            * `mbr_filter()`
            * `within_mbb()`
    * ###### teradataml GeoDataFrameColumn
      * Geospatial Specific Properties
        * ###### Properties for all Types of Geometries
          * boundary
          * centroid
          * convex_hell
          * coord_dim
          * dimension
          * geom_type
          * is_3D
          * is_empty
          * is_simple
          * is_valid
          * max_x
          * max_y
          * max_z
          * min_x
          * min_y
          * min_z
          * srid
        * ###### Properties for Point Geometry
          * x
          * y
          * z
        * ###### Properties for LineString Geometry
          * is_closed_3D
          * is_closed
          * is_ring
        * ###### Properties for Polygon Geometry
          * area
          * exterior
          * perimeter
      * Geospatial Specific Methods
        * ###### Methods for All Type of Geometry
          * `buffer()`
          * `contains()`
          * `crosses()`
          * `difference()`
          * `disjoint()`
          * `distance()`
          * `distance_3D()`
          * `envelope()`
          * `geom_equals()`
          * `intersection()`
          * `intersects()`
          * `make_2D()`
          * `mbb()`
          * `mbr()`
          * `overlaps()`
          * `relates()`
          * `set_exterior()`
          * `set_srid()`
          * `simplify()`
          * `sym_difference()`
          * `to_binary()`
          * `to_text()`
          * `touches()`
          * `transform()`
          * `union()`
          * `within()`
          * `wkb_geom_to_sql()`
          * `wkt_geom_to_sql()`
        * ###### Methods for Point Geometry
          * `spherical_buffer()`
          * `spherical_distance()`
          * `spheriodal_buffer()`
          * `spheriodal_distance()`
          * `set_x()`
          * `set_y()`
          * `set_z()`
        * ###### Methods for LineString Geometry
          * `endpoint()`
          * `length()`
          * `length_3D()`
          * `line_interpolate_point()`
          * `num_points()`
          * `point()`
          * `start_point()`
        * ###### Methods for Polygon Geometry
          * `interiors()`
          * `num_interior_ring()`
          * `point_on_surface()`
        * ###### Methods for GeometryCollection Geometry
          * `geom_component()`
          * `num_geometry()`
        * ###### Methods for GeoSequence Geometry
          * `clip()`
          * `get_final_timestamp()`
          * `get_init_timestamp()`
          * `get_link()`
          * `get_user_field()`
          * `get_user_field_count()`
          * `point_heading()`
          * `set_link()`
          * `speed()`
        * ###### Filtering Functions and Methods
          * `intersects_mbb()`
          * `mbb_filter()`
          * `mbr_filter()`
          * `within_mbb()`
  
  * ###### teradataml DataFrame
    * _New Functions_
      * `to_csv()`
    
  * ###### teradataml: SQLE Engine Analytic Functions
    * _New Functions_
      *  Newly added SQLE functions are accessible only after establishing the connection to Vantage.
      * `display_analytic_functions()` API displays all the available SQLE Analytic functions based on database version. 
      * ###### Functions Supported on DatabaseVersions: 16.20.x.x, 17.10.x.x, 17.05.x.x
        * `Antiselect()`
        * `Attribution()`
        * `DecisionForestPredict()`
        * `DecisionTreePredict()`
        * `GLMPredict()`
        * `MovingAverage()`
        * `NaiveBayesPredict()`
        * `NaiveBayesTextClassifierPredict()`
        * `NGramSplitter()`
        * `NPath()`
        * `Pack()`
        * `Sessionize()`
        * `StringSimilarity()`
        * `SVMParsePredict()`
        * `Unpack()`
      * ###### Functions Supported on DatabaseVersions: 17.10.x.x
        * `Antiselect()`
        * `Attribution()`
        * `BincoodeFit()`
        * `BncodeTransform()`
        * `CategoricalSummary()`
        * `ChiSq()`
        * `ColumnSummary()`
        * `ConvertTo()`
        * `DecisionForestPredict()`
        * `DecisionTreePredict()`
        * `GLMPredict()`
        * `FillRowId()`
        * `FTest()`
        * `Fit()`
        * `Transform()`
        * `GetRowsWithMissingValues()`
        * `GetRowsWithoutMissingValues()`
        * `MovingAverage()`
        * `Histogram()`
        * `NaiveBayesPredict()`      
        * `NaiveBayesTextClassifierPredict()`
        * `NGramSplitter()`
        * `NPath()`
        * `NumApply()`
        * `OneHotEncodingFit()`
        * `OneHotEncodingTransform()`
        * `OutlierFilterFit()`
        * `OutlierFilterTransform()`
        * `Pack()`
        * `PolynomialFeatuesFit()`
        * `PolynomialFeatuesTransform()`
        * `QQNorm()`
        * `RoundColumns()`
        * `RowNormalizeFit()`
        * `RowNormalizeTransform()`
        * `ScaleFit()`
        * `ScaleTransform()`  
        * `Sessionize()`
        * `SimpleImputeFit()`
        * `SimpleImputeTransform()`
        * `StrApply()`
        * `StringSimilarity()`
        * `SVMParsePredict()`
        * `UniVariateStatistics()`
        * `Unpack()`
        * `WhichMax()`
        * `WhichMin()`
        * `ZTest()`
  
  * ###### teradataml: General Functions
    * _New Functions_
      * Data Transfer Utility
        * `read_csv()`
  
  * ###### Operators
    * _New Functions_
      * Table Operators
        * `read_nos()`
        * `write_nos()`
  
  * ###### teradataml: Bring Your Own Model
    * _New Functions_
      * Model Cataloging
        * `get_license()`
        * `set_byom_catalog()`
        * `set_license()`
  
* ##### Updates
    * ###### teradataml: General Functions
      * Data Transfer Utility
        * `copy_to_sql()` - New argument "chunksize" added to load data in chunks.
        * Following Data Transfer Utility Functions updated to specify the number of Teradata sessions to open for data transfer using "open_session" argument:
          * `fastexport()`
          * `fastload()`
          * `to_pandas()`
  
    * ###### Operators
      * Following Set Operator Functions updated to work with Geospatial data:
        * `concat()`
        * `td_intersect()`
        * `td_expect()`
        * `td_minus()`

    * ###### teradataml: Bring Your Own Model
      * Model cataloging APIs mentioned below are updated to use session level parameters set by `set_byom_catalog()` and `set_license()` such as table name, schema name and license details respectively.
        * `delete_byom()`
        * `list_byom()`
        * `retrieve_byom()`
        * `save_byom()`
      * `view_log()` - Allows user to view BYOM logs.
  
* ##### Bug Fixes
  * CS0733758 - `db_python_package_details()` function is fixed to support latest STO release for pip and Python aliases used.
  * DataFrame `print()` issue related to `Response Row size is greater than the 1MB allowed maximum.` has been fixed to print the data with lot of columns.
  * New parameter "chunksize" is added to `DataFrame.to_sql()` and `copy_to_sql()` to fix the issue where the function was failing with error - "Request requires too many SPOOL files.". Reducing the chunksize than the default one will result in successful operation.
  * `remove_context()` is fixed to remove the active connection from database.
  * Support added to specify the number of Teradata data transfer sessions to open for data transfer using `fastexport()` and `fastload()` functions.
  * `DataFrame.to_sql()` is fixed to support temporary table when default database differs from the username. 
  * `DataFrame.to_pandas()` now by default support data transfer using regular method. Change is carried out for user to allow the data transfer if utility throttles are configured, i.e., TASM configuration does not support data export using FastExport.
  * `save_byom()` now notifies if VARCHAR column is trimmed out if data passed to the API is greater than the length of the VARCHAR column.
  * Standard error can now be captured for `DataFrame.map_row()` and `DataFrame.map_parition()` when executed in LOCAL mode.
  * Vantage Analytic Library - Underlying SQL can be retrieved using newly added arguments "gen_sql"/"gen_sql_only" for the functions. Query can be viewed with the help `show_query()`.
  * Documentation example has been fixed for `fastexport()` to show the correct import statement.
  

#### teradataml 17.00.00.05
Fixed [CS0733758] db_python_package_details() fails on recent STO release due to changes in pip and python aliases.


#### teradataml 17.00.00.04
* ##### New Features/Functionality
  * ###### Analytic Functions
    * Bring Your Own Analytics Functions
      The BYOM feature in Vantage provides flexibility to score the data in Vantage using external models using following BYOM functions:
      * `H2OPredict()` - Score using model trained externally in H2O and stored in Vantage.
      * `PMMLPredict()` - Score using model trained externally in PMML and stored in Vantage.
      * BYOM Model Catalog APIs
        * `save_byom()` - Save externally trained models in Teradata Vantage.
        * `delete_byom()` - Delete a model from the user specified table in Teradata Vantage.
        * `list_byom()` - List models.
        * `retrieve_byom()` - Function to retrieve a saved model.
    * Vantage Analytic Library Functions
      * _New Functions_
        * `XmlToHtmlReport()` - Transforms XML output of VAL functions to HTML.
  * ###### teradataml DataFrame
    * `DataFrame.window()` - Generates Window object on a teradataml DataFrame to run window aggregate functions.
    * `DataFrame.csum()` - Returns column-wise cumulative sum for rows in the partition of the dataframe.
    * `DataFrame.mavg()` - Returns moving average for the current row and the preceding rows.
    * `DataFrame.mdiff()` - Returns moving difference for the current row and the preceding rows.
    * `DataFrame.mlinreg()` - Returns moving linear regression for the current row and the preceding rows.
    * `DataFrame.msum()` - Returns moving sum for the current row and the preceding rows.
    * _Regular Aggregate Functions_
      * `DataFrame.corr()` - Returns the Sample Pearson product moment correlation coefficient.
      * `DataFrame.covar_pop()` - Returns the population covariance.
      * `DataFrame.covar_samp()` - Returns the sample covariance.
      * `DataFrame.regr_avgx()` - Returns the mean of the independent variable.
      * `DataFrame.regr_avgy()` - Returns the mean of the dependent variable.
      * `DataFrame.regr_count()` - Returns the count of the dependent and independent variable arguments.
      * `DataFrame.rege_intercept()` - Returns the intercept of the univariate linear regression line.
      * `DataFrame.regr_r2()` - Returns the coefficient of determination.
      * `DataFrame.regr_slope()` - Returns the slope of the univariate linear regression line through.
      * `DataFrame.regr_sxx()` - Returns the sum of the squares of the independent variable expression.
      * `DataFrame.regr_sxy()` - Returns the sum of the products of the independent variable and the dependent variable.
      * `DataFrame.regr_syy()` - Returns the sum of the squares of the dependent variable expression.
  * ###### teradataml DataFrameColumn a.k.a. ColumnExpression
    * `ColumnExpression.window()` - Generates Window object on a teradataml DataFrameColumn to run window aggregate functions.
    * `ColumnExpression.desc()` - Sorts ColumnExpression in descending order.
    * `ColumnExpression.asc()` - Sorts ColumnExpression in ascending order.
    * `ColumnExpression.distinct()` - Removes duplicate value from ColumnExpression.
    * _Regular Aggregate Functions_
      * `ColumnExpression.corr()` - Returns the Sample Pearson product moment correlation coefficient.
      * `ColumnExpression.count()` - Returns the column-wise count.
      * `ColumnExpression.covar_pop()` - Returns the population covariance.
      * `ColumnExpression.covar_samp()` - Returns the sample covariance.
      * `ColumnExpression.kurtosis()` - Returns kurtosis value for a column.
      * `ColumnExpression.median()` - Returns column-wise median value.
      * `ColumnExpression.max()` - Returns the column-wise max value.
      * `ColumnExpression.mean()` - Returns the column-wise average value.
      * `ColumnExpression.min()` - Returns the column-wise min value.
      * `ColumnExpression.regr_avgx()` - Returns the mean of the independent variable.
      * `ColumnExpression.regr_avgy()` - Returns the mean of the dependent variable.
      * `ColumnExpression.regr_count()` - Returns the count of the dependent and independent variable arguments.
      * `ColumnExpression.rege_intercept()` - Returns the intercept of the univariate linear regression line.
      * `ColumnExpression.regr_r2()` - Returns the coefficient of determination arguments.
      * `ColumnExpression.regr_slope()` - Returns the slope of the univariate linear regression line.
      * `ColumnExpression.regr_sxx()` - Returns the sum of the squares of the independent variable expression.
      * `ColumnExpression.regr_sxy()` - Returns the sum of the products of the independent variable and the dependent variable.
      * `ColumnExpression.regr_syy()` - Returns the sum of the squares of the dependent variable expression.
      * `ColumnExpression.skew()` - Returns skew value for a column.
      * `ColumnExpression.std()` - Returns the column-wise population/sample standard deviation.
      * `ColumnExpression.sum()` - Returns the column-wise sum.
      * `ColumnExpression.var()` - Returns the column-wise population/sample variance.
      * `ColumnExpression.percentile()` - Returns the column-wise percentile.
  * ###### teradataml Window - Window Aggregate Functions
    Following set of _Window Aggregate Functions_ return the results over a specified window which can be of any type:
      * Cumulative/Expanding window
      * Moving/Rolling window
      * Contracting/Remaining window
      * Grouping window
    _Window Aggregate Functions_
    * `Window.corr()` - Returns the Sample Pearson product moment correlation coefficient.
    * `Window.count()` - Returns the count.
    * `Window.covar_pop()` - Returns the population covariance.
    * `Window.covar_samp()` - Returns the sample covariance.
    * `Window.cume_dist()` - Returns the cumulative distribution of values.
    * `Window.dense_Rank()` - Returns the ordered ranking of all the rows.
    * `Window.first_value()` - Returns the first value of an ordered set of values.
    * `Window.lag()` - Returns data from the row preceding the current row at a specified offset value.
    * `Window.last_value()` - Returns the last value of an ordered set of values.
    * `Window.lead()` - Returns data from the row following the current row at a specified offset value.
    * `Window.max()` - Returns the column-wise max value.
    * `Window.mean()` - Returns the column-wise average value.
    * `Window.min()` - Returns the column-wise min value.
    * `Window.percent_rank()` - Returns the relative rank of all the rows.
    * `Window.rank()` - Returns the rank (1 … n) of all the rows.
    * `Window.regr_avgx()` - Returns the mean of the independent variable arguments.
    * `Window.regr_avgy()` - Returns the mean of the dependent variable arguments.
    * `Window.regr_count()` - Returns the count of the dependent and independent variable arguments.
    * `Window.rege_intercept()` - Returns the intercept of the univariate linear regression line arguments.
    * `Window.regr_r2()` - Returns the coefficient of determination arguments.
    * `Window.regr_slope()` - Returns the slope of the univariate linear regression line.
    * `Window.regr_sxx()` - Returns the sum of the squares of the independent variable expression.
    * `Window.regr_sxy()` - Returns the sum of the products of the independent variable and the dependent variable.
    * `Window.regr_syy()` - Returns the sum of the squares of the dependent variable expression.
    * `Window.row_number()` - Returns the sequential row number.
    * `Window.std()` - Returns the column-wise population/sample standard deviation.
    * `Window.sum()` - Returns the column-wise sum.
    * `Window.var()` - Returns the column-wise population/sample variance.
  * ###### General functions
    * _New functions_
      * `fastexport()` - Exports teradataml DataFrame to Pandas DataFrame using FastExport data transfer protocol.
  * ###### teradataml Options
    * Display Options
      * `display.blob_length`
        Specifies default display length of BLOB column in teradataml DataFrame.
    * Configuration Options
      * `configure.temp_table_database`
        Specifies database name for storing the tables created internally.
      * `configure.temp_view_database`
        Specifies database name for storing the views created internally.
      * `configure.byom_install_location`
        Specifies the install location for the BYOM functions.
      * `configure.val_install_location`
        Specifies the install location for the Vantage Analytic Library functions.
* ##### Updates
  * ###### teradataml DataFrame
    * `to_pandas()` - 
      * Support added to transfer data to Pandas DataFrame using fastexport protocol improving the performance.
      * Support added for other arguments similar to Pandas `read_sql()`:
        * `coerce_float`
        * `parse_dates`
  * ###### Analytic functions
    * Vantage Analytic Library Functions
      * Support added to accept datetime.date object for literals/values in 
        following transformation functions:
        * `FillNa()`
        * `Binning()`
        * `OneHotEncoder()`
        * `LabelEncoder()`
      * All transformation functions now supports accepting 
        teradatasqlalchemy datatypes as input to "datatype" argument for 
        casting the result.
* ##### Bug Fixes.
  * CS0249633 - Support added for teradataml to work with user/database/tablename
    containing period (.).
  * CS0086594 - Use of dbc.tablesvx versus dbc.tablesvx in teradatasqlalchemy.
  * IPython integration to print the teradataml DataFrames in pretty format.
  * teradataml DataFrame APIs now support column names same as that of Teradata 
    reserved keywords.
  * Issue has been fixed for duplicate rows being loaded via teradataml 
    fastload() API.
  * VAL - Empty string now can be passed as input for recoding values using 
    LabelEncoder.
  * teradataml extension with SQLAlchemy functions:
    * mod() function is fixed to return correct datatype.
    * sum() function is fixed to return correct datatype.
    

#### teradataml 17.00.00.03
- New release of SQLAlchemy1.4.x introduced backward compatibility issue. A fix has been carried out so that teradataml can support latest SQLAlchemy changes.
- Other minor bug fixes.

#### teradataml 17.00.00.02
Fixed the internal library load issue related to the GCC version discrepancies on CentOS platform.

#### teradataml 17.00.00.01
* ##### New Features/Functionality
  * ###### Analytic Functions
    * Vantage Analytic Library
      teradataml now supports executing analytic functions offered by Vantage Analytic Library.
      These functions are available via new 'valib' sub-package of teradataml.
      Following functions are added as part of this:
      * Association Rules:
        * `Association()`
      * Descriptive Statistics:
        * `AdaptiveHistogram()`
        * `Explore()`
        * `Frequency()`
        * `Histogram()`
        * `Overlaps()`
        * `Statistics()`
        * `TextAnalyzer()`
        * `Values()`
      * Decision Tree:
        * `DecisionTree()`
        * `DecisionTreePredict()`
        * `DecisionTreeEvaluator()`
      * Fast K-Means Clustering:
        * `KMeans()`
        * `KMeansPredict()`
      * Linear Regression:
        * `LinReg()`
        * `LinRegPredict()`
      * Logistic Regression:
        * `LogReg()`
        * `LogRegPredict()`
        * `LogRegEvaluator()`
      * Factor Analysis:
        * `PCA()`
        * `PCAPredict()`
        * `PCAEvaluator()`
      * Matrix Building:
        * `Matrix()`
      * Statistical Tests:
        * `BinomialTest()`
        * `ChiSquareTest()`
        * `KSTest()`
        * `ParametricTest()`
        * `RankTest()`
      * Variable Transformation:
        * `Transform()`
        * Transformation Techniques supported for variable transformation:
          * `Binning()` - Perform bin coding to replaces continuous numeric column with a
                          categorical one to produce ordinal values.
          * `Derive()` - Perform free-form transformation done using arithmetic formula.
          * `FillNa()` - Perform missing value/null replacement transformations.
          * `LabelEncoder()` - Re-express categorical column values into a new coding scheme.
          * `MinMaxScalar()` - Rescale data limiting the upper and lower boundaries.
          * `OneHotEncoder()` - Re-express a categorical data element as one or more
                                numeric data elements, creating a binary numeric field for each
                                categorical data value.
          * `Retain()` - Copy one or more columns into the final analytic data set.
          * `Sigmoid()` - Rescale data using sigmoid or s-shaped functions.
          * `ZScore()` - Rescale data using Z-Score values.
    * ML Engine Functions (mle)
      * Correlation2
      * NaiveBayesTextClassifier2
  * ###### DataFrame
    * _New Functions_
      * `DataFrame.map_row()` - Function to apply a user defined function to each row in the
                                teradataml DataFrame.
      * `DataFrame.map_partition()` - Function to apply a user defined function to a group or
                                      partition of rows in the teradataml DataFrame.
    * _New Property_
      * `DataFrame.tdtypes` - Get the teradataml DataFrame metadata containing column names and
                              corresponding teradatasqlalchemy types.
  * ###### General functions
    * _New functions_
      * Database Utility Functions
        * `db_python_package_details()` - Lists the details of Python packages installed on Vantage.
      * General Utility Functions
        * `print_options()`
        * `view_log()`
        * `setup_sandbox_env()`
        * `copy_files_from_container()`
        * `cleanup_sandbox_env()`
* ##### Updates
  * ###### `create_context()`
    * Supports all connection parameters supported by teradatasql.connect().
  * ###### Script
    * `test_script()` can now be executed in 'local' mode, i.e., outside of the sandbox.
    * `Script.setup_sto_env()` is deprecated. Use `setup_sandbox_env()` function instead.
    * Added support for using "quotechar" argument.
  * ###### Analytic functions
    * _Updates_
      * Visit teradataml User Guide to know more about the updates done to ML Engine analytic
        functions. Following type of updates are done to several functions:
        * New arguments are added, which are supported only on Vantage Version 1.3.
        * Default value has been updated for few function arguments.
        * Few arguments were required, but now they are optional.
* ##### Minor Bug Fixes.

#### teradataml 17.00.00.00
* ##### New Features/Functionality
  * ###### Model Cataloging - Functionality to catalog model metadata and related information in the Model Catalog.
    * `save_model()` - Save a teradataml Analytic Function model.
    * `retrieve_model()` - Retrieve a saved model.
    * `list_model()` - List accessible models.
    * `describe_model()` - List the details of a model.
    * `delete_model()` - Remove a model from Model Catalog.
    * `publish_model()` - Share a model.
  * ###### Script - An interface to the SCRIPT table operator object in the Advanced SQL Engine.
    Interface offers execution in two modes:
    * Test/Debug - to test user scripts locally in a containerized environment.
      Supporting methods:
      * `setup_sto_env()` - Set up test environment.
      * `test_script()` - Test user script in containerized environment.
      * `set_data()` - Set test data parameters.
    * In-Database Script Execution - to execute user scripts in database.
      Supporting methods:
      * `execute_script()` - Execute user script in Vantage.
      * `install_file()` - Install or replace file in Database.
      * `remove_file()` - Remove installed file from Database.
      * `set_data()` - Set test data parameters.
  * ###### DataFrame
    * `DataFrame.show_query()` - Show underlying query for DataFrame.
    * Regular Aggregates
      * _New functions_
        * `kurtosis()` - Calculate the kurtosis value.
        * `skew()` - Calculate the skewness of the distribution.
      * _Updates_\
        New argument `distinct` is added to following aggregates to exclude duplicate values.
        * `count()`
        * `max()`
        * `mean()`
        * `min()`
        * `sum()`
        * `std()`
          * New argument `population` is added to calculate the population standard deviation.
        * `var()`
          * New argument `population` is added to calculate the population variance.
    * Time Series Aggregates
      * _New functions_
        * `kurtosis()` - Calculate the kurtosis value.
        * `count()` - Get the total number of values.
        * `max()` - Calculate the maximum value.
        * `mean()` - Calculate the average value.
        * `min()` - Calculate the minimum value.
        * `percentile()` - Calculate the desired percentile.
        * `skew()` - Calculate the skewness of the distribution.
        * `sum()` - Calculate the column-wise sum value.
        * `std()` - Calculate the sample and population standard deviation.
        * `var()` - Calculate the sample and population standard variance.
  * ###### General functions
    * _New functions_
      * Database Utility Functions
        * `db_drop_table()`
        * `db_drop_view()`
        * `db_list_tables()`
      * Vantage File Management Functions
        * `install_file()` - Install a file in Database.
        * `remove_file()` - Remove an installed file from Database.
    * _Updates_
      * `create_context()`
        * Support added for Stored Password Protection feature.
        * Kerberos authentication bug fix.
        * New argument `database` added to `create_context()` API, that allows user to specify connecting database.
  * ###### Analytic functions
    * _New functions_
      * `Betweenness`
      * `Closeness`
      * `FMeasure`
      * `FrequentPaths`
      * `IdentityMatch`
      * `Interpolator`
      * `ROC`
    * _Updates_
      * New methods are added to all analytic functions
        * `show_query()`
        * `get_build_time()`
        * `get_prediction_type()`
        * `get_target_column()`
      * New properties are added to analytic function's Formula argument
        * `response_column`
        * `numeric_columns`
        * `categorical_columns`
        * `all_columns`

#### teradataml 16.20.00.06
Fixed the DataFrame data display corruption issue observed with certain analytic functions.

#### teradataml 16.20.00.05
Compatible with Vantage 1.1.1.\
The following ML Engine (`teradataml.analytics.mle`) functions have new and/or updated arguments to support the Vantage version:
* `AdaBoostPredict`
* `DecisionForestPredict`
* `DecisionTreePredict`
* `GLMPredict`
* `LDA`
* `NaiveBayesPredict`
* `NaiveBayesTextClassifierPredict`
* `SVMDensePredict`
* `SVMSparse`
* `SVMSparsePredict`
* `XGBoostPredict`

#### teradataml 16.20.00.04
* ##### Improvements
  * DataFrame creation is now quicker, impacting many APIs and Analytic functions.
  * Improved performance by reducing the number of intermediate queries issued to Teradata Vantage when not required.
    * The number of queries reduced by combining multiple operations into a single step whenever possible and unless the user expects or demands to see the intermediate results.
    * The performance improvement is almost proportional to the number of chained and unexecuted operations on a teradataml DataFrame.
  * Reduced number of intermediate internal objects created on Vantage.
* ##### New Features/Functionality
  * ###### General functions
    * _New functions_
      * `show_versions()` - to list the version of teradataml and dependencies installed.
      * `fastload()` - for high performance data loading of large amounts of data into a table on Vantage. Requires `teradatasql` version `16.20.0.48` or above.
      * Set operators:
        * `concat`
        * `td_intersect`
        * `td_except`
        * `td_minus`
      * `case()` - to help construct SQL CASE based expressions.
    * _Updates_
      * `copy_to_sql`
        * Added support to `copy_to_sql` to save multi-level index.
        * Corrected the type mapping for index when being saved.
      * `create_context()` updated to support 'JWT' logon mechanism.
  * ###### Analytic functions
    * _New functions_
      * `NERTrainer`
      * `NERExtractor`
      * `NEREvaluator`
      * `GLML1L2`
      * `GLML1L2Predict`
    * _Updates_
      * Added support to categorize numeric columns as categorical while using formula - `as_categorical()` in the `teradataml.common.formula` module.
  * ###### DataFrame
    * Added support to create DataFrame from Volatile and Primary Time Index tables.
    * `DataFrame.sample()` - to sample data.
    * `DataFrame.index` - Property to access `index_label` of DataFrame.
    * Functionality to process Time Series Data
      * Grouping/Resampling time series data:
        * `groupby_time()`
        * `resample()`
      * Time Series Aggregates:
        * `bottom()`
        * `count()`
        * `describe()`
        * `delta_t()`
        * `mad()`
        * `median()`
        * `mode()`
        * `first()`
        * `last()`
        * `top()`
    * DataFrame API and method argument validation added.
    * `DataFrame.info()` - Default value for `null_counts` argument updated from `None` to `False`.
    * `Dataframe.merge()` updated to accept columns expressions along with column names to `on`, `left_on`, `right_on` arguments.
  * ###### DataFrame Column/ColumnExpression methods
    * `cast()` - to help cast the column to a specified type.
    * `isin()` and `~isin()` - to check the presence of values in a column.
* ##### Removed deprecated Analytic functions
  * All the deprecated Analytic functions under the `teradataml.analytics module` have been removed.
    Newer versions of the functions are available under the `teradataml.analytics.mle` and the `teradataml.analytics.sqle` modules.
    The modules removed are:
    * `teradataml.analytics.Antiselect`
    * `teradataml.analytics.Arima`
    * `teradataml.analytics.ArimaPredictor`
    * `teradataml.analytics.Attribution`
    * `teradataml.analytics.ConfusionMatrix`
    * `teradataml.analytics.CoxHazardRatio`
    * `teradataml.analytics.CoxPH`
    * `teradataml.analytics.CoxSurvival`
    * `teradataml.analytics.DecisionForest`
    * `teradataml.analytics.DecisionForestEvaluator`
    * `teradataml.analytics.DecisionForestPredict`
    * `teradataml.analytics.DecisionTree`
    * `teradataml.analytics.DecisionTreePredict`
    * `teradataml.analytics.GLM`
    * `teradataml.analytics.GLMPredict`
    * `teradataml.analytics.KMeans`
    * `teradataml.analytics.NGrams`
    * `teradataml.analytics.NPath`
    * `teradataml.analytics.NaiveBayes`
    * `teradataml.analytics.NaiveBayesPredict`
    * `teradataml.analytics.NaiveBayesTextClassifier`
    * `teradataml.analytics.NaiveBayesTextClassifierPredict`
    * `teradataml.analytics.Pack`
    * `teradataml.analytics.SVMSparse`
    * `teradataml.analytics.SVMSparsePredict`
    * `teradataml.analytics.SentenceExtractor`
    * `teradataml.analytics.Sessionize`
    * `teradataml.analytics.TF`
    * `teradataml.analytics.TFIDF`
    * `teradataml.analytics.TextTagger`
    * `teradataml.analytics.TextTokenizer`
    * `teradataml.analytics.Unpack`
    * `teradataml.analytics.VarMax`

#### teradataml 16.20.00.03
* Fixed the garbage collection issue observed with `remove_context()` when context is created using a SQLAlchemy engine.
* Added 4 new Advanced SQL Engine (was NewSQL Engine) analytic functions supported only on Vantage 1.1:
    * `Antiselect`, `Pack`, `StringSimilarity`, and `Unpack`.
* Updated the Machine Learning Engine `NGrams` function to work with Vantage 1.1.

#### teradataml 16.20.00.02
* Python version 3.4.x will no longer be supported. The Python versions supported are 3.5.x, 3.6.x, and 3.7.x.
* Major issue with the usage of formula argument in analytic functions with Python3.7 has been fixed, allowing this package to be used with Python3.7 or later.
* Configurable alias name support for analytic functions has been added.
* Support added to create_context (connect to Teradata Vantage) with different logon mechanisms.
    Logon mechanisms supported are: 'TD2', 'TDNEGO', 'LDAP' & 'KRB5'.
* copy_to_sql function and DataFrame 'to_sql' methods now provide following additional functionality:
    * Create Primary Time Index tables.
    * Create set/multiset tables.
* New DataFrame methods are added: 'median', 'var', 'squeeze', 'sort_index', 'concat'.
* DataFrame method 'join' is now updated to make use of ColumnExpressions (df.column_name) for the 'on' clause as opposed to strings.
* Series is supported as a first class object by calling squeeze on DataFrame.
    * Methods supported by teradataml Series are: 'head', 'unique', 'name', '\_\_repr__'.
    * Binary operations with teradataml Series is not yet supported. Try using Columns from teradataml.DataFrames.
* Sample datasets and commands to load the same have been provided in the function examples.
* New configuration property has been added 'column_casesenitive_handler'. Useful when one needs to play with case sensitive columns.

#### teradataml 16.20.00.01
* New support has been added for Linux distributions: Red Hat 7+, Ubuntu 16.04+, CentOS 7+, SLES12+.
* 16.20.00.01 now has over 100 analytic functions. These functions have been organized into their own packages for better control over which engine to execute the analytic function on. Due to these namespace changes, the old analytic functions have been deprecated and will be removed in a future release. See the Deprecations section in the Teradata Python Package User Guide for more information.
* New DataFrame methods `shape`, `iloc`, `describe`, `get_values`, `merge`, and `tail`.
* New Series methods for NA checking (`isnull`, `notnull`) and string processing (`lower`, `strip`, `contains`).

#### teradataml 16.20.00.00
* `teradataml 16.20.00.00` is the first release version. Please refer to the _Teradata Python Package User Guide_ for a list of Limitations and Usage Considerations.

## Installation and Requirements

### Package Requirements:
* Python 3.5 or later

Note: 32-bit Python is not supported.

### Minimum System Requirements:
* Windows 7 (64Bit) or later
* macOS 10.9 (64Bit) or later
* Red Hat 7 or later versions
* Ubuntu 16.04 or later versions
* CentOS 7 or later versions
* SLES 12 or later versions
* Teradata Vantage Advanced SQL Engine:
    * Advanced SQL Engine 16.20 Feature Update 1 or later
* For a Teradata Vantage system with the ML Engine:
    * Teradata Machine Learning Engine 08.00.03.01 or later

### Installation

Use pip to install the Teradata Python Package for Advanced Analytics.

Platform       | Command
-------------- | ---
macOS/Linux    | `pip install teradataml`
Windows        | `py -3 -m pip install teradataml`

When upgrading to a new version of the Teradata Python Package, you may need to use pip install's `--no-cache-dir` option to force the download of the new version.

Platform       | Command
-------------- | ---
macOS/Linux    | `pip install --no-cache-dir -U teradataml`
Windows        | `py -3 -m pip install --no-cache-dir -U teradataml`

## Using the Teradata Python Package

Your Python script must import the `teradataml` package in order to use the Teradata Python Package:

```
>>> import teradataml as tdml
>>> from teradataml import create_context, remove_context
>>> create_context(host = 'hostname', username = 'user', password = 'password')
>>> df = tdml.DataFrame('iris')
>>> df

   SepalLength  SepalWidth  PetalLength  PetalWidth             Name
0          5.1         3.8          1.5         0.3      Iris-setosa
1          6.9         3.1          5.1         2.3   Iris-virginica
2          5.1         3.5          1.4         0.3      Iris-setosa
3          5.9         3.0          4.2         1.5  Iris-versicolor
4          6.0         2.9          4.5         1.5  Iris-versicolor
5          5.0         3.5          1.3         0.3      Iris-setosa
6          5.5         2.4          3.8         1.1  Iris-versicolor
7          6.9         3.2          5.7         2.3   Iris-virginica
8          4.4         3.0          1.3         0.2      Iris-setosa
9          5.8         2.7          5.1         1.9   Iris-virginica

>>> df = df.select(['Name', 'SepalLength', 'PetalLength'])
>>> df

              Name  SepalLength  PetalLength
0  Iris-versicolor          6.0          4.5
1  Iris-versicolor          5.5          3.8
2   Iris-virginica          6.9          5.7
3      Iris-setosa          5.1          1.4
4      Iris-setosa          5.1          1.5
5   Iris-virginica          5.8          5.1
6   Iris-virginica          6.9          5.1
7      Iris-setosa          5.1          1.4
8   Iris-virginica          7.7          6.7
9      Iris-setosa          5.0          1.3

>>> df = df[(df.Name == 'Iris-setosa') & (df.PetalLength > 1.5)]
>>> df

          Name  SepalLength  PetalLength
0  Iris-setosa          4.8          1.9
1  Iris-setosa          5.4          1.7
2  Iris-setosa          5.7          1.7
3  Iris-setosa          5.0          1.6
4  Iris-setosa          5.1          1.9
5  Iris-setosa          4.8          1.6
6  Iris-setosa          4.7          1.6
7  Iris-setosa          5.1          1.6
8  Iris-setosa          5.1          1.7
9  Iris-setosa          4.8          1.6
```

## Documentation

General product information, including installation instructions, is available in the [Teradata Documentation website](https://docs.teradata.com/search/documents?query=package+python+-lake&filters=category~%2522Programming+Reference%2522_%2522User+Guide%2522*prodname~%2522Teradata+Package+for+Python%2522_%2522Teradata+Python+Package%2522&sort=last_update&virtual-field=title_only&content-lang=)

## License

Use of the Teradata Python Package is governed by the *License Agreement for the Teradata Python Package for Advanced Analytics*. 
After installation, the `LICENSE` and `LICENSE-3RD-PARTY` files are located in the `teradataml` directory of the Python installation directory.
