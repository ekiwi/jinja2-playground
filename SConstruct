import os

env = Environment(
		toolpath = ['site_tools'],
		tools = ['template'],
		ENV = os.environ)


class Generator:
	def __init__(self, env, basepath):
		self.env = env
		self.basepath = basepath
	def template(self, target, source, substitutions):
		dd = self.env.Jinja2Template(
						target = os.path.join(self.basepath, target),
						source = os.path.join(self.basepath, source),
						substitutions = substitutions)
		self.env.Alias('template', dd)
		return dd

env['TemplateGenerator'] = Generator

# Add files (normally done in SConscript.generate file)
substitutions = {
	'a': 12,
	'b': 15,
	'c': 'Hello World'
}

generator = env['TemplateGenerator'](env, '')	# env, directory
generator.template('generated/test.cpp', 'test.cpp.in', substitutions)

env.Alias('templates', 'template')
env.Default('template')
