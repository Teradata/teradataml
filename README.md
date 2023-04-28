## Teradata Python package for Advanced Analytics.

teradataml makes available to Python users a collection of analytic functions that reside on Teradata Vantage. This allows users to perform analytics on Teradata Vantage with no SQL coding. In addition, the teradataml library provides functions for scaling data manipulation and transformation, data filtering and sub-setting, and can be used in conjunction with other open-source python libraries.

For community support, please visit the [Teradata Community](https://support.teradata.com/community?id=community_forum&sys_id=14fe131e1bf7f304682ca8233a4bcb1d).

For Teradata customer support, please visit [Teradata Support](https://support.teradata.com/csm).

Copyright 2023, Teradata. All Rights Reserved.

### Table of Contents
* [Release Notes](#release-notes)
* [Installation and Requirements](#installation-and-requirements)
* [Using the Teradata Python Package](#using-the-teradata-python-package)
* [Documentation](#documentation)
* [License](#license)

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
