++++++++++++++++++++++++++++++++++++++++
Align: polite, proper sequence alignment
++++++++++++++++++++++++++++++++++++++++

    :Authors: Marcin Cieślik, Brent Pedersen (brentp), Wibowo Arindrarto (bow)
    :Email: (marcin), bpederse@gmail.com, bow@bow.web.id
    :License: BSD

.. contents ::


About
=====
Various packages implement sequence alignment algorithms with various levels of
success. This package is an attempt to handle the sequence alignment properly,
including edge-cases.

Use [Cython](http://cython.org/) and [numpy](http://www.numpy.org/) under the hood.

Installation
============
In a (dino)python virtualenv :

    git clone https://github.com/brentp/align.git
    cd align
    python setup.py install


Usage
=====

usage will change. currently ::

    from align.matrix import DNAFULL
    from align import aligner

    print(aligner('WW','WEW', method= 'global'))
    # [AlignmentResult(seq1=b'W-W', seq2=b'WEW', start1=0, start2=0, end1=2, end2=3, n_gaps1=1, n_gaps2=0, n_mismatches=0, score=15.0)]

    print(aligner('WW','WEWWEW', method= 'glocal'))
    # [AlignmentResult(seq1=b'WW', seq2=b'WW', start1=0, start2=2, end1=2, end2=4, n_gaps1=0, n_gaps2=0, n_mismatches=0, score=22.0)]

    print(aligner('TAATTC', 'TAAT', method='global', matrix=DNAFULL, gap_open=-10, gap_extend=-1))
    # [AlignmentResult(seq1=b'TAATTC', seq2=b'TAAT--', start1=0, start2=0, end1=6, end2=4, n_gaps1=0, n_gaps2=1, n_mismatches=0, score=9.0)]

    print(aligner('PYNCHAN', 'YNCH', method='local'))
    # [AlignmentResult(seq1=b'YNCH', seq2=b'YNCH', start1=1, start2=0, end1=5, end2=4, n_gaps1=0, n_gaps2=0, n_mismatches=0, score=30.0)]

    alm = aligner('AAAAAAAAAAAAACCTGCGCCCCAAAAAAAAAAAAAAAAAAAA', 'CCTGCGCACCCC', method='global_cfe')
    assert alm[0].seq1 == 'AAAAAAAAAAAAACCTGCGC-CCCAAAAAAAAAAAAAAAAAAAA'
    assert alm[0].seq2 == '-------------CCTGCGCACCCC-------------------'

