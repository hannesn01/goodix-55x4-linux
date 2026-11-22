
sigfm_sources = ['sigfm.cpp']

# 'opencv4' was renamed to 'opencv5' in the opencv 5.1 Arch package;
# accept the old name when present (e.g. on opencv 5.0 systems), fall back to the new one.
opencv = dependency('opencv4', required: false)
if not opencv.found()
    opencv = dependency('opencv5', required: true)
endif
doctest = dependency('doctest', required: false, version: ['>=2.0.0', '<3.0.0'])

libsigfm = static_library('sigfm',
        sigfm_sources,
        dependencies: [opencv],
)

sigfm_match_tests = executable('sigfm-match-tests', 'test-match.cpp',
        dependencies: [glib_dep, opencv], link_with: libsigfm)
test('sigfm-match', sigfm_match_tests, suite: 'unit-tests')

# doctest ships header-only with no pkg-config file on some distros; only build
# the unit tests when it is actually available so the library still configures.
if doctest.found()
        sigfm_tests = executable('sigfm-tests', ['./tests.cpp'], dependencies: [doctest, opencv], link_with: [libsigfm])
endif
