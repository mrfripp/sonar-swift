# Using with Fastlane 🚀

If you already use Fastlane, you can simply setup a new lane performing the analysis as follows:

```ruby
lane :metrics do
    scan(scheme: "[SCHEME]", code_coverage: true, derived_data_path: "./DerivedData", output_directory: "./reports")
    slather(cobertura_xml: true, jenkins: true, scheme: "[SCHEME]", build_directory: "./DerivedData", output_directory: "./reports", proj: "./[PROJECT].xcodeproj")
    sh("cd .. && lizard ./[SOURCE_FOLDER] -l swift --xml > ./reports/lizard-report.xml")
    swiftlint(output_file: "./reports/swiftlint.txt", ignore_exit_status: true)
    sonar
end

```

## Options

Fastlane's `sonar` action allows you to define or override a number of SonarQube properties, such as `sonar.project-version`.

For instance:

```ruby
  sonar(project_version: "1.0b")
```

You can read the complete documentation of Fastlane's `sonar` action on your terminal via:

```bash
  fastlane action sonar
```

## `sonar-project.properties`

Please note that, in order to have your analysis performed via the tools above, you'll need to setup your `sonar-project.properties` file accordingly, as per the following example.

```
sonar.junit.reportsPath=reports/
sonar.junit.include=*.junit
sonar.swift.lizard.report=reports/lizard-report.xml
sonar.swift.coverage.reportPattern=reports/cobertura.xml
sonar.swift.swiftlint.report=reports/*swiftlint.txt
```
