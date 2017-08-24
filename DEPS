use_relative_paths = True

vars = {
  'chromium_git': 'https://chromium.googlesource.com',

  'build_revision': 'bee933aa41e29016998f5fbdd05cc2ce457e28c5',
  'buildtools_revision': 'f90f6a5af3e8cf843395bfe6243cf606f71b5344',
  'gmock_revision': '29763965ab52f24565299976b936d1265cb6a271',
  'gtest_revision': '8245545b6dc9c4703e6496d1efd19e975ad2b038',

  'base_revision': '9f243792c0d8ae1fe77d07941ea2cb7646f0d359',

  'icu_revision': '08cb956852a5ccdba7f9c941728bb833529ba3c6',
  'skia_revision': 'e0e20755f6c09b71038ced2bf4a00b4c4593f504',
  'icu_revision': '08cb956852a5ccdba7f9c941728bb833529ba3c6',
  'clang_revision': 'a1420b85586c1fa3eaf68808bbb095334d2d271d',
  'gen_library_loader_revision': '916d4acd8b2cde67a390737dfba90b3c37de23a1',
  'libfuzzer_revision': 'be060c214102e6ce94a3f9a9841d197266d4af7c',

  'modp_revision': '28e3fbba4cb4ec3ffd85b53d0a3904525d08f5a6',
  'zlib_revision': '718f686437b89038ac83525f4f1b1888aadd9bfc',
  'compact_enc_det_revision': '368a9cc09ad868a3d28f0b5ad4a733f263c46409'
}

deps = {
  "build":
    Var('chromium_git') + "/chromium/src/build.git@" + Var('build_revision'),

  "buildtools":
    Var('chromium_git') + "/chromium/buildtools.git@" +
        Var('buildtools_revision'),
  "testing/gmock":
    Var('chromium_git') + "/external/googlemock.git@" + Var('gmock_revision'),

  "testing/gtest":
    Var('chromium_git') + "/external/googletest.git@" + Var('gtest_revision'),

  "testing/libfuzzer":
    Var('chromium_git') + "/chromium/src/testing/libfuzzer@" +  Var('libfuzzer_revision'),

  "tools/clang":
    Var('chromium_git') + "/chromium/src/tools/clang@" +  Var('clang_revision'),
  #
  "base" :
    Var('chromium_git') + "/chromium/src/base@" + Var('base_revision'),

  "third_party/icu":
    Var('chromium_git') + "/chromium/deps/icu.git@" + Var('icu_revision'),

  "third_party/modp_b64":
    Var('chromium_git') + "/chromium/src/third_party/modp_b64@" + Var('modp_revision'),

  "third_party/zlib":
    Var('chromium_git') + "/chromium/src/third_party/zlib@" + Var('zlib_revision'),
  'third_party/ced/src':
    (Var("chromium_git")) + '/external/github.com/google/compact_enc_det.git@' + Var('compact_enc_det_revision'),
}

recursedeps = [
  # buildtools provides clang_format, libc++, and libc++abi
  'buildtools',
]

include_rules = [
  # Basic stuff that everyone can use.
  # Note: public is not here because core cannot depend on public.
  '+testing'
  '+/base/base'
]

hooks = [
  {
    'name': 'gn_win',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=win32',
                '--no_auth',
                '--bucket', 'chromium-gn',
                '-s', 'googlebase/buildtools/win/gn.exe.sha1',
    ],
  },

  # Pull clang-format binaries using checked-in hashes.
  {
    'name': 'clang_format_win',
    'pattern': '.',
    'action': [ 'download_from_google_storage',
                '--no_resume',
                '--platform=win32',
                '--no_auth',
                '--bucket', 'chromium-clang-format',
                '-s', 'googlebase/buildtools/win/clang-format.exe.sha1',
    ],
  },

  {
    # Pull clang
    'name': 'clang',
    'pattern': '.',
    'action': ['python',
               'googlebase/tools/clang/scripts/update.py'
    ],
  },
]