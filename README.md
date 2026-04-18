from biosignal import DataLoader, Preprocessor, FeatureExtractor, StabilityAnalyzer

data = DataLoader.from_apple_watch("export.xml")

processed = Preprocessor(data).filter().resample().quality_check()

features = FeatureExtractor(processed)\
    .compute_entropy()\
    .compute_hrv()\
    .compute_complexity()

analyzer = StabilityAnalyzer(features)

risk_score = analyzer.compute_risk_score()
warnings = analyzer.detect_early_warnings()
