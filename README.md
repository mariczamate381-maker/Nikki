// embedded_core/lib/models/adas_model.dart (Дополнение)

// Конечный автомат: этапы системы помощи при парковке
enum ParkingState {
  off, // Система выключена
  searching, // Поиск подходящего места
  spotEvaluated, // Место найдено и оценено (ждет подтверждения водителя)
  activeManeuvering, // Активное выполнение маневров (автоматическое управление)
  emergencyBraking, // Аварийная остановка (обнаружено критическое препятствие)
  maneuverComplete, // Парковка завершена, ждет P (парковка)
}

// Запланированная траектория (Добавление индекса для отслеживания прогресса)
class Trajectory {
  final List<TrajectoryPoint> points;
  final int currentPointIndex; // Точка, к которой стремится автомобиль

  Trajectory({required this.points, this.currentPointIndex = 0});
  
  bool get isFinished => currentPointIndex >= points.length;
}

// Расширение Obstacle для более детальной визуализации
class Obstacle {
  final String id;
  final double distanceCm;
  final double lateralOffsetCm;
  final HazardLevel hazard;
  final double collisionProbability; // 0.0 до 1.0 (новая метрика)
  
  Obstacle({
    required this.id, required this.distanceCm, required this.lateralOffsetCm, 
    this.hazard = HazardLevel.none, this.collisionProbability = 0.0
  });
}
