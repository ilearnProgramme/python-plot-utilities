# plot_utils.category_means

**plot_utils.category_means**(_categorical_array, continuous_array, fig=None, ax=None, figsize=(3,3), dpi=100, title=None, xlabel=None, ylabel=None, rot=0, dropna=False, show_stats=True, **violinplot_kwargs_):

Summarize the mean values of entries of y corresponding to each distinct
category in x, and show a violin plot to visualize it. The violin plot will
show the distribution of y values corresponding to each category in x.

Also, a one-way ANOVA test (H0: different categories in x yield same
average y values) is performed, and F statistics and p-value are returned.

#### [Parameters]
    categorical_array : <array_like>
        An vector of categorical values.
    continuous_array : <array_like>
        The target variable whose values correspond to the values in x. Must
        have the same length as x. It is natural that y contains continuous
        values, but if y contains categorical values (expressed as integers,
        not strings), this function should also work.
    fig, ax : <mpl.figure.Figure>, <mpl.axes._subplots.AxesSubplot>
        Figure and axes objects.
        If provided, the histograms are plotted on the provided figure and
        axes. If not, a new figure and new axes are created.
    figsize : tuple of two scalars
        Size (width, height) of figure in inches. (fig object passed via "fig"
        will over override this parameter)
    dpi : scalar
        Screen resolution. (fig object passed via "fig" will over override
        this parameter)
    title : <str>
        The title of the violin plot, usually the name of vector x.
    xlabel : <str>
        The label for the x axis (i.e., categories) of the violin plot. If None
        and x is a pandas Series, use x's 'name' attribute as xlabel.
    ylabel : <str>
        The label for the y axis (i.e., average y values) of the violin plot.
        If None and y is a pandas Series, use y's 'name' attribute as ylabel.
    rot : <float>
        The rotation (in degrees) of the x axis labels.
    show_stats : <bool>
        Whether or not to show the statistical test results (F statistics
        and p-value) on the figure.
    **violinplot_kwargs :
        Keyword arguments to be passed to plt.violinplot().
        (https://matplotlib.org/api/_as_gen/matplotlib.axes.Axes.violinplot.html)
        Note that this subroutine overrides the default behavior of violinplot:
        showmeans is overriden to True and showextrema to False.

#### [Returns]
    fig, ax :
        Figure and axes objects
    mean_values : <dict>
        A dictionary whose keys are the categories in x, and their corresponding
        values are the mean values in y.
    F_stat : <float>
        The computed F-value of the one-way ANOVA test.
    p_value : <float>
        The associated p-value from the F-distribution.

-----------------------------------------

# plot_utils.positive_rate

**plot_utils.positive_rate**(*categorical_array, two_classes_array, fig=None, ax=None, figsize='auto', dpi=100, barh=True, top_n=-1, dropna=False, xlabel='Positive rate', ylabel='Categories', show_stats=True*):

Calculate the proportions of the different categories in vector x that fall
into class "1" (or "True") in vector y, and optionally show a figure.

Also, a Pearson's chi-squared test is performed to test the independence
between x and y. The chi-squared statistics, p-value, and degree-of-freedom
are returned.

#### [Parameters]
    categorical_array : <array_like>
        An vector of categorical values
    two_class_array : <array_like>
        The target variable containing two classes. Each value in y correspond
        to a value in x (at the same index). Must have the same length as x.
        The second unique value in y will be considered as the positive class
        (for example, "True" in [True, False, True], or "3" in [1,1,3,3,1]).
    fig, ax : <mpl.figure.Figure>, <mpl.axes._subplots.AxesSubplot>
        Figure and axes objects.
        If provided, the histograms are plotted on the provided figure and
        axes. If not, a new figure and new axes are created.
    figsize : tuple of two scalars, or 'auto'
        Size (width, height) of figure in inches. (fig object passed via "fig"
        will over override this parameter). If 'auto', the figure size will be
        automatically determined from the number of distinct categories in x.
    dpi : scalar
        Screen resolution. (fig object passed via "fig" will over override
        this parameter)
    barh : <bool>
        Whether or not to show the bars as horizontal (otherwise, vertical).
    top_n : <int>
        Only shows top_n categories (ranked by their positive rate) in the
        figure. Useful when there are too many categories.
    dropna : <bool>
        If True, ignore entries (in both arrays) where there are missing values
        in at least one array. If False, the missing values are treated as a
        new category, "N/A".
    show_stats : <bool>
        Whether or not to show the statistical test results (chi2 statistics
        and p-value) on the figure.
        
#### [Returns]
    fig, ax :
        Figure and axes objects
    pos_rate : <pd.Series>
        The positive rate of each categories in x.

-----------------------------------------

# plot_utils.contingency_table

**plot_utils.contingency_table**(*array_horizontal, array_vertical, fig=None, ax=None, figsize='auto', dpi=100, color_map='auto', xlabel=None, ylabel=None, dropna=False, rot=45, normalize=True, symm_cbar=True, show_stats=True*):

Calculate and visualize the contingency table from two categorical arrays.
Also perform a Pearson's chi-squared test to evaluate whether the two arrays
are independent.

#### [Parameters]
    array_horizontal : <array_like>
        Array to show as the horizontal margin in the contigency table (i.e.,
        its categories are the column headers)
    array_vertical : <array_like>
        Array to show as the vertical margin in the contigency table (i.e.,
        its categories are the row names)
    fig, ax : <mpl.figure.Figure>, <mpl.axes._subplots.AxesSubplot>
        Figure and axes objects.
        If provided, the histograms are plotted on the provided figure and
        axes. If not, a new figure and new axes are created.
    figsize : tuple of two scalars, or 'auto'
        Size (width, height) of figure in inches. (fig object passed via "fig"
        will over override this parameter). If 'auto', the figure size will be
        automatically determined from the number of distinct categories in x.
    dpi : scalar
        Screen resolution. (fig object passed via "fig" will over override
        this parameter)
    color_map : <str> or <matplotlib.colors.Colormap>
        The color scheme specifications. Valid names are listed in
        https://matplotlib.org/users/colormaps.html.
        If relative_color is True, use diverging color maps (e.g., PiYG, PRGn,
        BrBG, PuOr, RdGy, RdBu, RdYlBu, RdYlGn, Spectral, coolwarm, bwr,
        seismic). Otherwise, use sequential color maps (e.g., viridis, jet).
    xlabel : <str>
        The label for the horizontal axis. If None and x is a pandas Series,
        use x's 'name' attribute as xlabel.
    ylabel : <str>
        The label for the vertical axis. If None and y is a pandas Series, use
        y's 'name' attribute as ylabel.
    dropna : <bool>
        If True, ignore entries (in both arrays) where there are missing values
        in at least one array. If False, the missing values are treated as a
        new category, "N/A".
    rot : <float> or 'vertical' or 'horizontal'
        The rotation of the x axis labels.
    normalize : <bool>
        If True, plot the contingency table as the relative difference between
        the observed and the expected (i.e., (obs. - exp.)/exp. ). If False,
        plot the original "observed frequency".
    symm_cbar : <bool>
        If True, the limits of the color bar are symmetric. Otherwise, the
        limits are the natural minimum/maximum of the table to be plotted.
        It has no effect if "normalize" is set to False.
    show_stats : <bool>
        Whether or not to show the statistical test results (chi2 statistics
        and p-value) on the figure.

#### [Returns]
    fig, ax :
        Figure and axes objects
    chi2_results : <tuple>
        A tuple in the order of (chi2, p_value, degree_of_freedom)
