# Recipes for H2O Driverless AI

## About Driverless AI and BYOR 
See main [README](https://github.com/h2oai/driverlessai-recipes/README.md)

## About Data Recipes
Driverless AI allows you to create a new dataset by modifying an existing dataset with a data recipe. 
When inside **Dataset Details** page click the **Modify by Recipe** button in the top right portion of the UI, then click **Live Code** from the submenu that appears.
The Dialog Box that appears will feature an editor to enter the code for the data recipe you want to use to modify the dataset. The list of templates below are designed
for the live code applications with certain modifications specific to the dataset they apply to.

## Reference Guide
* [Adding a Data Recipe](http://docs.h2o.ai/driverless-ai/latest-stable/docs/userguide/custom-recipes-data-recipes.html#adding-a-data-recipe)
* [Templates](https://github.com/h2oai/driverlessai-recipes/blob/master/FAQ.md#references)
* [Technical Architecture Diagram](https://raw.githubusercontent.com/h2oai/driverlessai-recipes/master/reference/DriverlessAI_BYOR.png)

## Sample Recipes
[Go to Recipes for Driverless 1.7.0](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.7.0)
 [1.7.1](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.7.1)
 [1.8.0](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.8.0)
 [1.8.1](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.8.1)
 [1.8.2](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.8.2)
 [1.8.3](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.8.3)
 [1.8.4](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.8.4)
 [1.8.5](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.8.5)
 [1.8.6](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.8.6)
 [1.8.7](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.8.7)
 [1.8.8](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.8.8)
 [1.9.0](https://github.com/h2oai/driverlessai-recipes/tree/rel-1.9.0)
### Count: 21
      * [balance_data.py](./data/livecode//balance_data.py) [ Create a sampled dataset for imbalanced use cases - probably not for modeling but
         can be nice to better see trends in MLI PDP plots
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
           target_col: str - usually target column to use when balancing data
           times: int - how much to downsample majority class: in number of times size of minority class
           random_seed: int - random seed to control for reproducibility
         Output:
           dataset with downsampled majority class
        ]
      * [bind_2_datasets.py](./data/livecode//bind_2_datasets.py) [ Livecode for binding 2 datasets' rows (rbind). Datasets should have the same
         columnar structure, e.g. train dataset and test dataset (with target present).
         For more details see docs on datatable's Frame.rbind() here:
         https://datatable.readthedocs.io/en/latest/api/frame.html#datatable.Frame.rbind
        
         Specification:
         Inputs:
           X: datatable - primary dataset
           X2_name: datatable - dataset to bind with
         Parameters:
           None
         Output:
           dataset containing all rows from both datasets
        ]
      * [bind_X_and_y.py](./data/livecode//bind_X_and_y.py) [ Livecode for binding 2 datasets with the same number of rows, e.g.
         one dataset with features and another dataset has target.
         Recipe won't perform any joins/mapping but rather stitch
         2 datasets' rows together.
        ]
      * [bind_n_datasets.py](./data/livecode//bind_n_datasets.py) [ Livecode for binding multiple datasets' rows (rbind). Datasets should have the same
         columnar structure, e.g. each file contains one month of train data.
         For more details see docs on datatable's Frame.rbind() here:
         https://datatable.readthedocs.io/en/latest/api/frame.html#datatable.Frame.rbind
        
         Specification:
         Inputs:
           X: datatable - primary dataset
           files_to_bind: list of datatables - datasets to bind with
         Parameters:
           None
         Output:
           dataset containing all rows from primary and the list datasets
        ]
      * [compute_shift_diff_per_column.py](./data/livecode//compute_shift_diff_per_column.py) [ Compute per-column difference between current and previous (shift)
         values for each time series - both by time groups (multiple time
         series) and across covariates (multivariate time series).
         Multiple time series identified by group columns while 
         covariates are explicitly assigned in `shift_cols`.
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
           time_col: date/time/int - time column to order rows before the shift op
           group_by_cols: list of column names - group columns
           shift_cols: list of column names - columns to shift
         Output:
           dataset augmented with shifted columns
        ]
      * [compute_stats_by_groups_per_column.py](./data/livecode//compute_stats_by_groups_per_column.py) [ Compute per-column expressions (signed distance from the mean in this example) 
         for all numeric (int, float) columns with stats computed by groups and
         new column added for each original numeric feature.
         see: https://stackoverflow.com/questions/62974899/updating-or-adding-multiple-columns-with-pydatatable-in-style-of-r-datables-sd
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
           group_by_cols: list of column names - group columns to compute stats by
         Output:
           dataset augmented with computed statistics
        ]
      * [create_time_interval_partition.py](./data/livecode//create_time_interval_partition.py) [ Extract single partition based on time interval
         Data is called X and is a DataTable object
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
           date_col: date/time/int - time column to order rows
           split_date_min: lower bound of partition interval
           split_date_max: upper bound of partition interval
         Output:
           dataset containing partition interval
        ]
      * [drop_duplicates.py](./data/livecode//drop_duplicates.py) [ Remove duplicate rows by grouping the same rows,
         sorting them and then selecting first (1) or last (-1)
         row from each group
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
           sort_cols: date/time/int/str - column(s) to order rows within each group
           key_cols: list of column names - group columns
         Output:
           dataset after removing dups
        ]
      * [fill_ts.py](./data/livecode//fill_ts.py) [ Add any missing Group by Date records and fill with a default value -
         additional columns will be null for the default values
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
           ts_col: date/time - temporal column
           group_by_cols: list of columns - column(s) to define groups of rows
           target_col: list of column names - group columns
           default_missing_value: - value to fill when missing found
         Output:
           dataset augmented with missing data
        ]
      * [filter_columns_by_types.py](./data/livecode//filter_columns_by_types.py) [ Filter only columns of certain types. Beware that column order
         changes after filtering. For more details see f-expressions in 
         datatable docs: 
         https://datatable.readthedocs.io/en/latest/manual/f-expressions.html#f-expressions
         E.g. below all integer and floating-point columns are retained 
         while the others are dropped. Because int type is followed by
         float type columns are re-shuffled so all integer columns 
         placed first and then float ones.
         For reference various data type filters are listed.
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
        
         Output:
           dataset with columns filtered by data types
        ]
      * [find_mli_rowids.py](./data/livecode//find_mli_rowids.py) [ Get interesting RowIDs to search for in MLI
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
           target_col: list of column names - group columns
         Output:
           dataset with selected rows and ids
        ]
      * [impute_X.py](./data/livecode//impute_X.py) [ Live code recipe for imputing all missing values
         in a dataset
         If you don't want certain data type to be filled just 
         change its filler's value to None
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
           fill_numeric: numeric - filler for missing numeric values
           fill_char:  string - filler for missing string values
           fill_bool: bool - filler for missing logical values
         Output:
           dataset with filled values
        ]
      * [insert_unique_id.py](./data/livecode//insert_unique_id.py) [ Livecode to add (insert) new column containing unique row
         identifier. New dataset will be identical to its source
         plus inserted first column containing unique ids from 0 to N-1
        
         Specification:
         Inputs:
           X: datatable - primary data set
         Parameters:
           column_name: string - new column name to store id values
         Output:
           dataset augmented with id column
        ]
      * [join_X_left_outer_Y.py](./data/livecode//join_X_left_outer_Y.py) [ Livecode for joining 2 datasets, e.g.
         one dataset with transactions and another dataset has extended set of features.
         find location of the dataset file by going to DETAILS where it's displayed
         on top under dataset name
        
         Specification:
         Inputs:
           X: datatable - primary dataset
           Y_name: datatable - dataset to bind with
         Parameters:
           join_key: string - column name to use as a key in join
         Output:
           dataset containing all rows from both datasets
        ]
      * [map_target_to_binary_outcome.py](./data/livecode//map_target_to_binary_outcome.py) [ Maps multi-nominal target (outcome) to binomial target column by
         binding new column to a dataset (new dataset will be created).
         For example, use when working with multi-nominal classifier and want 
         to see if binomial model may be preferred or compliment use case.
        
         Specification:
         Inputs:
           X: datatable - primary dataset
         Parameters:
           target_name: string - target column name
           new_target_name: string - new target column name
           value_to_map_to_true: value - target values that maps to binary positive (true) outcome
           binary_outcomes: tuple - pair of binary outcomes to sue for new target
           drop_old_target: bool - if true then drop old target column
         Output:
           dataset containing all rows from both datasets
        ]
      * [melt_X.py](./data/livecode//melt_X.py) [ Change dataset format from wide to long using melt function
         Identify id columns and value columns to use Pandas melt 
         function
        
         Specification:
         Inputs:
           X: datatable - primary dataset
         Parameters:
           id_cols: list of columns - columns to use as identifier variables
           value_col_regex: string - regular expression pattern to select value columns
           value_cols: list of columns - columns to unpivot (melt) to use (if regex 'value_col_regex' is None)
           var_name: string - name to use for the 'variable' columns
           value_name: string - name to use for the 'value' column
         Output:
           dataset containing all rows from both datasets
        ]
      * [pivot_X.py](./data/livecode//pivot_X.py) [ Change dataset format from long to wide using pivot function
         Identify id columns and value columns to use Pandas pivot 
         function
        
         Specification:
         Inputs:
           X: datatable - primary dataset
         Parameters:
           id_cols: list of columns - column to use to make new frame’s index
           var_name: string - name to use for the 'variable' columns
           value_name: string - name to use for the 'value' column
         Output:
           dataset containing all rows from both datasets
        ]
      * [rename_column_names.py](./data/livecode//rename_column_names.py) [ Rename column name(s) in the dataset
        
         Specification:
         Inputs:
           X: datatable - primary dataset
         Parameters:
           column_rename_map: dictionary - dictionary mapping old column names to new ones
        ]
      * [sample_X.py](./data/livecode//sample_X.py) [ Random sample of rows from X
        
         Specification:
         Inputs:
           X: datatable - primary dataset
         Parameters:
           fraction: float - fraction of rows to sample from 'X' (must be between 0 and 1)
           random_seed: int - random seed to control for reproducibility
        ]
      * [split_by_datetime.py](./data/livecode//split_by_datetime.py) [ Data is called X and is a DataTable object
        
         Specification:
         Inputs:
           X: datatable - primary dataset
         Parameters:
           date_col: string - name of temporal column
           split_date: date/time - temporal value to split dataset on
        ]
      * [split_dataset_by_partition_column.py](./data/livecode//split_dataset_by_partition_column.py) [ Split dataset by partition id (column): results in as many partitions (datasets)
         as there are values in parition column
        
         Specification:
         Inputs:
           X: datatable - primary dataset
         Parameters:
           partition_col_name: string - column name identifying which partition row belongs to
           dataset_name_prefix: string - prefix to use in the names for new datasets
           MAX_PARTITIONS: int - maximum number of partition datasets to create
        ]