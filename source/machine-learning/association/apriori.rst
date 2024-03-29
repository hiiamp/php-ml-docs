Apriori Associator
==================

Association rule learning based on `Apriori
algorithm <https://en.wikipedia.org/wiki/Apriori_algorithm>`__ for
frequent item set mining.

Constructor Parameters
~~~~~~~~~~~~~~~~~~~~~~

-  $support - minimum threshold of
   `support <https://en.wikipedia.org/wiki/Association_rule_learning#Support>`__,
   i.e. the ratio of samples which contain both X and Y for a rule "if X
   then Y"
-  $confidence - minimum threshold of
   `confidence <https://en.wikipedia.org/wiki/Association_rule_learning#Confidence>`__,
   i.e. the ratio of samples containing both X and Y to those containing
   X

::

    use Phpml\Association\Apriori;

    $associator = new Apriori($support = 0.5, $confidence = 0.5);

Train
~~~~~

To train a associator simply provide train samples and labels (as
``array``). Example:

::

    $samples = [['alpha', 'beta', 'epsilon'], ['alpha', 'beta', 'theta'], ['alpha', 'beta', 'epsilon'], ['alpha', 'beta', 'theta']];
    $labels  = [];

    use Phpml\Association\Apriori;

    $associator = new Apriori($support = 0.5, $confidence = 0.5);
    $associator->train($samples, $labels);

You can train the associator using multiple data sets, predictions will
be based on all the training data.

Predict
~~~~~~~

To predict sample label use ``predict`` method. You can provide one
sample or array of samples:

::

    $associator->predict(['alpha','theta']);
    // return [['beta']]

    $associator->predict([['alpha','epsilon'],['beta','theta']]);
    // return [[['beta']], [['alpha']]]

Associating
~~~~~~~~~~~

Get generated association rules simply use ``rules`` method.

::

    $associator->getRules();
    // return [['antecedent' => ['alpha', 'theta'], 'consequent' => ['beta'], 'support' => 1.0, 'confidence' => 1.0], ... ]

Frequent item sets
~~~~~~~~~~~~~~~~~~

Generating k-length frequent item sets simply use ``apriori`` method.

::

    $associator->apriori();
    // return [ 1 => [['alpha'], ['beta'], ['theta'], ['epsilon']], 2 => [...], ...]

